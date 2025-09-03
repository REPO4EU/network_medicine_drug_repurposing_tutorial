# Tutorial: Network medicine-based drug repurposing

## Setup
> [!TIP]
> 
> **Windows**
> 
> The easiest way to get the setup running on Windows is to work completely through the **[Windows Subsystem for Linux (WSL)](https://documentation.ubuntu.com/wsl/latest/howto/install-ubuntu-wsl2/)**.
> Alternatively, you can work with the dependencies in [`environment.windows.yaml`](environment.windows.yaml) for most hands-on tasks.

Clone the repository:
```bash  
git clone --recurse-submodules https://github.com/REPO4EU/network_medicine_drug_repurposing_tutorial.git
```

Enter the downloaded folder:
```bash  
cd network_medicine_drug_repurposing_tutorial
```

After cloning the repository, install the required packages using [conda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html) and the environment.yaml file: 
```bash  
conda env create -f environment.yaml
```

Activate the environment:
```bash  
conda activate network_medicine_tutorial
```

Register the environment as a jupyter kernel:

```
python -m ipykernel install --user --name network_medicine_tutorial --display-name "network_medicine_tutorial"
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
Install [Docker](https://docs.docker.com/engine/install/) if you do not have it already. If you are not using Linux, check the tips in the box below!

> [!TIP]
> **OS specifics**
> 
> Nextflow works best in combination with Linux. Furthermore, some Docker images in the pipeline are natively only available for `amd64` but not the `arm` architecture.
> Here are some tips to get the pipeline running with a different OS or architecture:
>
> **macOS**
> 
> With macOS and Apple silicon, we had better experiences using the free version of [orbstack](https://orbstack.dev/download) instead of Docker Desktop for deploying the containers.
>
>  **Windows**
>
> You will have to work through the [Windows Subsystem for Linux (WSL)](https://documentation.ubuntu.com/wsl/latest/howto/install-ubuntu-wsl2/).
> 
> **What if it keeps failing?**
>
> Most pipeline steps are not essential. If the pipeline keeps failing because of a specific process, you may be able to just [skip](https://nf-co.re/diseasemodulediscovery/dev/docs/usage/#skipping-steps) that one.
>
> If you cannot produce any pipeline outputs, you can still work on most hands-on tasks by using the [result files](data/nextflow_pipeline) we provide.


Now, run the pipeline with the test profile to verify that the setup works:

```bash  
nextflow run nf-core/diseasemodulediscovery -r dev -profile docker,test --outdir test_results
```

The first run may take some time because Nextflow needs to pull the software dependency containers. Subsequent runs should be significantly faster.
