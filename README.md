# Tutorial: Network medicine-based drug repurposing

## Setup
Clone the repository:
```bash  
git clone https://github.com/REPO4EU/network_medicine_drug_repurposing_tutorial.git
```

After cloning the repository, install the required packages using [conda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html) and the environment.yaml file: 
```bash  
conda env create -f environment.yaml
```

Activate the environment:
```bash  
conda activate network_medicine_tutorial
```

Launch the jupyter sever to start working on the hands-on projects:
```bash  
jupyter lab
```

### Nextflow pipeline setup
Activate the environment (Nextflow is already installed there):

```bash  
conda activate network_medicine_tutorial
```

Install [Docker](https://docs.docker.com/engine/install/) if you do not have it already.

Now, run the pipeline with the test profile to verify that the setup works:

```bash  
nextflow run nf-core/diseasemodulediscovery -r dev -profile docker,test --outdir test_results
```

The first run may take some time because Nextflow needs to pull the software dependency containers. Subsequent runs should be significantly faster.