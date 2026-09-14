# CH-315 Modeling Lab — Computational Carpentry Project

## Project information

**Course:** CH-315 Modeling Lab  
**Project:** Computational Carpentry Project  
**Group:** Group [LETTER]

### Team members

- [First name and surname]
- [First name and surname]
- [First name and surname]

## Project overview

This repository contains the group project for the Computational Carpentry module of CH-315.

The project is divided into three parts:

1. **Data structures and functions**
   - Load periodic-table data with pandas.
   - Create a dictionary containing atomic masses.
   - Calculate molecular masses.
   - Handle parentheses in chemical formulas.
   - Handle hydration water in formulas.

2. **Stoichiometry and reaction balancing**
   - Balance chemical reactions using linear algebra.
   - Verify mass conservation.

3. **Simulation and modeling**
   - Estimate π using a Monte Carlo simulation.
   - Simulate chemistry-inspired molecular collisions.
   - Estimate a reaction probability from collision energies.

The final notebook must contain the code, results, explanations and interpretations for every question.

## Repository contents

```text
.
├── Group[LETTER]_Block1_project.ipynb
├── periodic_table.csv
├── requirements.txt
├── README.md
└── .gitattributes
```

The repository structure may evolve during the project.

## Prerequisites

Each collaborator needs:

- Git
- Anaconda or Miniconda
- VS Code
- The Microsoft Python extension
- The Microsoft Jupyter extension

Do not use `github.com` or `github.dev` to execute the notebook with a local environment. Clone the repository and open it in VS Code Desktop.

## Clone the repository

```bash
git clone <REPOSITORY-URL>
cd <REPOSITORY-NAME>
```

Replace `<REPOSITORY-URL>` and `<REPOSITORY-NAME>` with the actual repository information.

## Create the Conda environment

Every collaborator must use the same environment name and Python version.

```bash
conda create -n mod_lab python=3.12 -y
conda activate mod_lab
```

Verify that the correct Python environment is active:

```bash
python --version
python -c "import sys; print(sys.executable)"
```

The executable path should contain:

```text
anaconda3\envs\mod_lab\python.exe
```

## Install the dependencies

With `mod_lab` activated, run:

```bash
python -m pip install -r requirements.txt
```

The minimal `requirements.txt` is:

```text
numpy
pandas
matplotlib
```

Add `scipy` only if the project imports it. It is not required when reaction balancing is performed with `numpy.linalg.svd`.

## Register the Jupyter kernel

Install `ipykernel` inside the environment:

```bash
conda activate mod_lab
python -m pip install ipykernel
```

Register the environment as a Jupyter kernel:

```bash
python -m ipykernel install --user --name mod_lab --display-name "Python (mod_lab)"
```

Open the project notebook in VS Code and select:

```text
Select Kernel
→ Select Another Kernel
→ Python Environments
→ mod_lab
```

If `mod_lab` is not displayed, press `Ctrl+Shift+P`, choose **Python: Select Interpreter**, and select:

```text
C:\Users\<USERNAME>\anaconda3\envs\mod_lab\python.exe
```

Replace `<USERNAME>` with your Windows username.

## Verify the notebook environment

Run the following cell at the beginning of the notebook:

```python
import sys
import numpy as np
import pandas as pd
import matplotlib

print("Python executable:", sys.executable)
print("Python version:", sys.version)
print("NumPy version:", np.__version__)
print("pandas version:", pd.__version__)
print("Matplotlib version:", matplotlib.__version__)
```

The Python executable should point to the `mod_lab` environment.

## Reproducible random simulations

Use a fixed random seed for the Monte Carlo simulations:

```python
import numpy as np

rng = np.random.default_rng(42)
```

Using the same seed allows all collaborators to reproduce the same random results.

## Notebook metadata cleaning

Jupyter notebooks contain outputs, execution counts and temporary metadata. These elements produce unnecessary Git differences and increase the risk of conflicts.

This repository uses `nbstripout` to remove them from the version committed to GitHub.

The local notebook remains unchanged and retains its outputs.

### Initial repository configuration

This step must be performed once by the person configuring the repository:

```bash
conda activate mod_lab
python -m pip install nbstripout
nbstripout --install --attributes .gitattributes
```

Commit the `.gitattributes` file:

```bash
git add .gitattributes
git commit -m "Configure notebook metadata cleaning"
git push
```

### Configuration for every collaborator

Every collaborator must activate the filter after cloning the repository:

```bash
conda activate mod_lab
python -m pip install nbstripout
nbstripout --install
```

Remove additional environment-specific notebook metadata:

```bash
git config filter.nbstripout.extrakeys "metadata.kernelspec metadata.language_info metadata.celltoolbar metadata.toc"
```

Verify the configuration:

```bash
nbstripout --status
```

The cleaning filter is automatically applied when a notebook is staged with `git add`.

## Branch-based collaboration workflow

The `main` branch must always contain the latest stable and working version of the project.

Collaborators should not work directly on `main`. Each new task must be completed on a separate branch and merged through a pull request.

### Branch naming convention

Use a short branch name containing the collaborator’s name and task:

```text
enea/part-a
alice/part-b
marie/part-c
enea/fix-formula-parser
alice/add-reaction-tests
```

Do not use spaces in branch names.

### Start a new task

Before creating a branch, update the local `main` branch:

```bash
git switch main
git pull --ff-only origin main
```

Create a new branch:

```bash
git switch -c <name>/<task>
```

Example:

```bash
git switch -c enea/part-a
```

Confirm the current branch:

```bash
git branch --show-current
```

### Work and commit on the branch

After modifying and testing the files:

```bash
git status
git add <modified-files>
git commit -m "Implement molecular mass calculator"
```

Push the branch to GitHub:

```bash
git push -u origin <name>/<task>
```

Example:

```bash
git push -u origin enea/part-a
```

The `-u` option connects the local branch to the corresponding GitHub branch. After the first push, the shorter command is sufficient:

```bash
git push
```

### Open a pull request

On GitHub:

1. Open the repository.
2. Click **Compare & pull request**.
3. Confirm that:
   - the base branch is `main`;
   - the source branch is the collaborator’s branch.
4. Give the pull request a clear title.
5. Briefly describe:
   - what was implemented;
   - which files were modified;
   - how the work was tested.
6. Ask another group member to review it.
7. Merge only after the notebook runs correctly.

Example pull request description:

```text
Implemented Part A molecular-mass calculation.

Changes:
- Loaded periodic_table.csv with pandas.
- Created the atomic-mass dictionary.
- Added the molecular_mass() function.
- Added tests for H2O, CO2 and C6H12O6.

The notebook cells run without errors using the mod_lab kernel.
```

### After a pull request is merged

Return to `main` and download the merged changes:

```bash
git switch main
git pull --ff-only origin main
```

Create a new branch from this updated version for the next task. Do not continue new work on an already merged branch.

## Avoiding notebook conflicts

Using branches does not completely prevent conflicts in `.ipynb` files. A notebook is stored as a large JSON document, so two people modifying different cells can still produce a Git conflict.

### Recommended parallel workflow

When several people need to work simultaneously, use separate draft notebooks:

```text
drafts/part_a_enea.ipynb
drafts/part_b_alice.ipynb
drafts/part_c_marie.ipynb
```

Each collaborator:

1. creates a personal task branch;
2. modifies only their assigned draft notebook;
3. commits and pushes the branch;
4. opens a pull request;
5. explains and tests their contribution.

A designated integrator then creates an integration branch:

```bash
git switch main
git pull --ff-only origin main
git switch -c integration/final-notebook
```

The integrator copies the completed Markdown and code cells from the draft notebooks into:

```text
Group[LETTER]_Block1_project.ipynb
```

The integration branch is reviewed and merged into `main` only after the final notebook runs from beginning to end.

### Alternative: edit the final notebook sequentially

If everyone wants to work directly in the final notebook, only one person may edit it at a time.

The sequence should be:

1. Collaborator A creates a branch, completes a section and merges it.
2. Collaborator B updates `main`, creates a new branch and completes the next section.
3. Collaborator C repeats the same process.

Never create three simultaneous branches that all modify:

```text
Group[LETTER]_Block1_project.ipynb
```

### If `main` changes while working

Update the task branch before opening the pull request:

```bash
git fetch origin
git merge origin/main
```

Resolve any conflicts, test the notebook, and commit the resolution:

```bash
git add <resolved-files>
git commit -m "Merge latest main into task branch"
git push
```

Do not edit raw notebook JSON unless you understand its structure. If a notebook conflict is complicated, keep both versions, open them separately in Jupyter, and manually copy the correct cells into a clean notebook.

## Daily Git checklist

Before working:

```bash
git switch main
git pull --ff-only origin main
git switch -c <name>/<task>
```

After working:

```bash
git status
git add <modified-files>
git commit -m "Clear description of the work"
git push -u origin <name>/<task>
```

Then open a pull request on GitHub.

## Important Git rules

- Never work directly on `main`.
- Never use `git push --force`.
- Always update `main` before creating a branch.
- Use one branch for one clearly defined task.
- Make small commits with clear messages.
- Do not modify the final notebook simultaneously.
- Test the notebook before opening a pull request.
- Review another person’s pull request before merging.
- Keep notebook outputs and metadata out of Git with `nbstripout`.
- Run the final notebook locally before submitting it to Moodle.