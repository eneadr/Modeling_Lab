# CH-315 Modeling Lab — Block 3 Project

## Project Overview

This project uses Kernel Ridge Regression (KRR) to predict CO₂ uptake in metal-organic frameworks (MOFs) from their structural and chemical descriptors.

The workflow includes exploratory data analysis, baseline models, feature scaling, hyperparameter optimization, feature selection, model evaluation and interpretation.

## Project Files

- `GroupG_Block3_Project.ipynb` — Complete notebook containing the code, results and explanations.
- `data/data.csv` — Dataset used for model training and evaluation.
- `assets/` — Figures and illustrations used in the notebook.
- `requirements.txt` — Required Python packages.
- `best_krr_model.joblib` — Saved optimized KRR pipeline.
- `LICENSE` — Original project license.

## Environment and Kernel Setup

The project was developed using **Python 3.12** in a Conda environment named `mod_lab`, with a Jupyter kernel registered under the same name.

### 1. Create the Conda environment

If the environment does not already exist, open a terminal and run:

```bash
conda create -n mod_lab python=3.12 -y
conda activate mod_lab
```

If `mod_lab` already exists, simply activate it:

```bash
conda activate mod_lab
```

### 2. Register the Jupyter kernel

To make the environment available in JupyterLab or VS Code:

```bash
python -m pip install ipykernel
python -m ipykernel install --user --name mod_lab --display-name "mod_lab"
```

The environment and kernel are now both named `mod_lab`.

### 3. Install the dependencies

The first code cell of the notebook contains:

```python
%pip install -r requirements.txt
```

This installs the required packages directly into the active kernel's Python environment. It should be executed before the import statements.

If packages have just been installed or updated, restart the kernel before continuing.

### 4. Run the notebook

1. Open the complete project folder in VS Code or JupyterLab.
2. Open `GroupG_Block3_Project.ipynb`.
3. Select the **`mod_lab`** kernel.
4. Make sure the notebook can access the `data/`, `assets/` and `requirements.txt` files.
5. Execute the cells in order, starting with dependency installation.

On **EPFL NOTO**, select a compatible kernel and install any missing packages using the first notebook cell. If `mod_lab` is not available, it must first be created and registered, provided the platform supports custom environments.

**Note:** Hyperparameter optimization and permutation importance can be computationally expensive. Their execution time depends on the available resources.

## License

The original project license is preserved in `LICENSE`.