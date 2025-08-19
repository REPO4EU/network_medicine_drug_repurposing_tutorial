# Nextflow pipeline for drug repurposing: hands-on

Before starting these hands-on tasks, ensure that you have completed the [Nextflow pipeline setup](../README.md/#nextflow-pipeline-setup)
.

The pipeline runs through the command line, so you do not need a Jupyter server for this session.

To begin, open a CLI and navigate to this subfolder:

```bash  
cd <path/to/repo>/nextflow_pipeline
```

## Task 1: Run the pipeline on the Huntington's Disease data

<details markdown="1">
<summary>Solution</summary>

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


<details markdown="1">
<summary>Solution</summary>

</details>