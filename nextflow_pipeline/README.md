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

Run the [nf-core/diseasemodulediscovery](https://nf-co.re/diseasemodulediscovery/dev/) pipeline using the Huntington's Disease-associated proteins as seeds and the PPI queried from NeDRex as network. To obtain results quickly, skip the evaluation workflow, as it is the most time-consuming step. Like this, the pipeline should finish in a few minutes.

> [!NOTE]
> The pipeline is still under development. To run it, include the `-r dev` parameter.
> 
> The ID space needs to be set to  `uniprot` to match the input.
> 
> You can skip the evaluation workflow using the `--skip_evaluation` flag.


<details markdown="1">
<summary> Solution </summary>

```bash  
nextflow run nf-core/diseasemodulediscovery \
-r dev -profile docker \
--seeds ../data/NeDRex_api/seed_genes_huntingtons_disease.csv \
--network ../data/NeDRex_api/filtered_ppi_only_reviewed_proteins_solution.csv \
--id_space uniprot \
--outdir results \
--skip_evaluation
```

</details>

## Task 2: Run the evaluation workflow
Once the run from Task 1 is complete, we have our first results to examine.
Next, let’s run the evaluation workflow by resuming the previous pipeline run without skipping the evaluation. This will make use of cached processes.

> [!NOTE]
> A pipeline run can be resumed by providing the `-resume` flag.

<details markdown="1">
<summary> Solution </summary>

```bash  
nextflow run nf-core/diseasemodulediscovery \
-r dev -profile docker \
--seeds ../data/NeDRex_api/seed_genes_huntingtons_disease.csv \
--network ../data/NeDRex_api/filtered_ppi_only_reviewed_proteins_solution.csv \
--id_space uniprot \
--outdir results \
-resume
```

</details>

You don't need to wait until this resumed run finishes, but can continue with Task 3, which does not need the additional results.

## Task 3: MultiQC report 

## Task 4: Run the seed input perturbation 

## Task 5: Module similarity and functional coherence

## Task 6: Robustness and seed rediscovery


<details markdown="1">
<summary> Solution </summary>

</details>