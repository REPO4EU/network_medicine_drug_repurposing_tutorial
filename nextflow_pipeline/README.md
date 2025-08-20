# Nextflow pipeline for drug repurposing: hands-on

Before starting these hands-on tasks, ensure that you have completed the [Nextflow pipeline setup](../README.md/#nextflow-pipeline-setup)
.

The pipeline runs through the command line, so you do not need a Jupyter server for this session.

To begin, open a CLI and navigate to this subfolder:

```bash  
cd <path/to/repo>/nextflow_pipeline
```

Please refer to the pipeline's [usage documentation](https://nf-co.re/diseasemodulediscovery/dev/docs/usage/), [parameter documentation](https://nf-co.re/diseasemodulediscovery/dev/parameters/), and [output documentation](https://nf-co.re/diseasemodulediscovery/dev/docs/output/) to solve the tasks.

> [!NOTE]
> The configuration file `nextflow.config` defines custom memory requirements optimized for the provided input data. By default, it limits Nextflow to a maximum of `12 GB` of memory. If your system offers significantly more or less memory, you can adjust this value in line 2.

## Task 1: Run the pipeline on the Huntington's Disease data

Run the [nf-core/diseasemodulediscovery](https://nf-co.re/diseasemodulediscovery/dev/) pipeline using the Huntington's Disease-associated proteins as seeds and the PPI queried from NeDRex as network. To obtain results quickly, skip slow processes like DIGEST and the module annotation. Like this, the pipeline should finish in a couple of minutes.

> [!NOTE]
> The pipeline is still under development. To run it, include the `-r dev` parameter.
> 
> The ID space needs to be set to  `uniprot` to match the input.
> 
> You can skip the DIGEST using the `--skip_digest` flag.
> 
> You can skip the module annotation using the `--skip_annotation` flag.


<details markdown="1">
<summary> Solution </summary>

```bash  
nextflow run nf-core/diseasemodulediscovery \
-r dev -profile docker \
--seeds ../data/NeDRex_api/seed_genes_huntingtons_disease.csv \
--network ../data/NeDRex_api/filtered_ppi_only_reviewed_proteins_solution.csv \
--id_space uniprot \
--skip_digest \
--skip_annotation \
--outdir results 
```

</details>

## Task 2: Run the seed permutation workflow
Once the run from Task 1 is complete, we have our first results to examine.
Next, let’s run the seed permutation workflow by resuming the previous pipeline run. This will make use of cached processes.

> [!NOTE]
> The seed permutation-based evaluation workflow does not run per default. Enable it using the `--run_seed_permutation` flag.
>
> A pipeline run can be resumed by providing the `-resume` flag.


<details markdown="1">
<summary> Solution </summary>

```bash  
nextflow run nf-core/diseasemodulediscovery \
-r dev -profile docker \
--seeds ../data/NeDRex_api/seed_genes_huntingtons_disease.csv \
--network ../data/NeDRex_api/filtered_ppi_only_reviewed_proteins_solution.csv \
--id_space uniprot \
--skip_digest \
--skip_annotation \
--outdir results \
--run_seed_permutation \
-resume
```

</details>

You don’t need to wait until the seed permutation analysis completes. You can go ahead with Task 3, which doesn’t require the additional results.

## Task 3: Exploring the output

> [!NOTE]
> Because NeDRex is continuously updated and some methods in the pipeline involve randomness, your results may not exactly match the provided solutions.

**Check the MultiQC pipeline report (`results/multiqc/multiqc_report.html`) to answer the following questions:**

How many nodes and edges are in the input network?

<details markdown="1">
<summary> Solution </summary>

> This information can be found in the **Input/Network** section of the MultiQC report.
> The used input network has **~12.800 nodes** and **~95.900 edges**.
</details>

What is the diameter of the input network?

<details markdown="1">
<summary> Solution </summary>

> The input network diameter is **10** and can be found in the same section of the MultiQC report.
> The diameter represents the longest shortest path between any two nodes in the network.
> For a PPI network, a diameter of 10 is relatively large. Unfiltered, larger PPIs are typically much denser, with diameters around 6.

</details>

Which method returns the largest disease module?

<details markdown="1">
<summary> Solution </summary>

> This information can be found in the **General Statistics** section of the MultiQc report.
> The **1st Neighbors** approach produces by far the largest disease modules, both in terms of nodes and edges.
> This is due to the high density of PPI networks and the occurrence of high-degree hub nodes. 
> Consequently, 1st Neighbor modules may contain a very large number of nodes, so their specificity should be interpreted with caution.

</details>

Which method removes the most seed nodes from its module?

<details markdown="1">
<summary> Solution </summary>

> This information can be found in the **General Statistics** section of the MultiQc report as well.
> The number of included `Seeds` is lowest for **DOMINO**, as it often excludes seed nodes from its modules.
> This can be advantageous if the seed set is noisy, but undesirable when working with a high-confidence gene selection.

</details>

Which disease modules have the most similar node sets?

<details markdown="1">
<summary> Solution </summary>

> You can find the relevant results in the **Overlap** section of the MultiQC report, which visualizes overlaps between disease module node sets using heatmaps. 
> Several configurations are available: overlaps can be quantified either by the number of shared nodes or by the Jaccard index. In addition, overlaps are also computed after removing the seed nodes, as these are expected to be present in the modules by default.
> The strongest similarity (based on the Jaccard index) is observed between the modules derived with **RWR and ROBUST**.

</details>

**In the MultiQC report, click on the Drugst.One export link of the random walk with restart (RWR) module to explore it through the Drugst.One web interface. Enable displaying adjacent drugs.**

Are there any drugs that directly target the mutant huntingtin (HTT) protein?

<details markdown="1">
<summary> Solution </summary>

> Adjacent drugs can be displayed using `Drugs` button in the right scroll menu.
> Currently, there are **no drugs** that directly target HTT, which motivates the use of network medicine approaches to identify alternative candidates.
> While some drugs do target other seed nodes, many are associated with nodes added during module construction. These may represent promising new therapeutic targets.

</details>

**Let's now check which drugs are network-based approach suggests based on the RWR module. For this, vave a look at the `results/drug_prioritization/drugstone/*.rwr.trustrank.drug_predictions.tsv` file.**

Which compounds have the highest TrustRank score (column `score`) for the RWR disease module?

<details markdown="1">
<summary> Solution </summary>

> Two compounds achieve the highest TrustRank score of 1: **Econazole and Miconazole**, both commonly used as antifungal agents. Their high ranking arises from the fact that they target the seed protein CNR1 (UniProt: P21554) as well as several additional nodes within the module.
> But does it really make sense to treat Huntington’s disease with antifungal drugs? At the very least, this is questionable. These are only algorithmic suggestions and must be carefully evaluated and prioritized by biomedical experts.

</details>

## Task 4: Robustness and seed rediscovery

Which method is most robust towards the leave-one-out seed set perturbation? 

<details markdown="1">
<summary> Solution </summary>

</details>

Which method is most depended on some individual seed nodes? 

<details markdown="1">
<summary> Solution </summary>

</details>

Which method performs best at recovering the left-out seed nodes?

<details markdown="1">
<summary> Solution </summary>

</details>

Which seed node is most frequently recovered?

<details markdown="1">
<summary> Solution </summary>

</details>