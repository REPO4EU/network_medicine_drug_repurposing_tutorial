**# Session 1: Databases - Option 2: NeDRex Python Package

## 1. Setup (If not already done)
**If you already followed the general setup you can skip Step 1 and go to Step 2!**

Clone the repository:
```bash  
git clone https://github.com/REPO4EU/network_medicine_drug_repurposing_tutorial.git
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

## Step 2: Use created environment

1. Activate the environment (if not already done):

```bash  
conda activate network_medicine_tutorial
```

2. Use jupyter server or your preferred IDE (e.g. PyCharm, VSCode) to work on the notebooks


**Jupyter server Option:** 

- Launch the jupyter sever to start working on the hands-on projects: Run: `jupyter lab`

- Navigate to the notebook of interest and start working on it