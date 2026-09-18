# CH-315 Modeling Lab — Computational Carpentry Project

## Project information

**Course:** CH-315 Modeling Lab  
**Project:** Computational Carpentry Project  
**Group:** GroupG

### Team members

| First name(s) | Surname | SCIPER | EPFL email | Git branch |
|---|---|---:|---|---|
| Marie | Lacroix | 372543 | marie.lacroix@epfl.ch | `marie` |
| Chloé | Baruselli | 363236 | chloe.baruselli@epfl.ch | `chloe` |
| Bertille Astrid Marie | Delloye | 397727 | bertille.delloye@epfl.ch | `bertille` |
| Enéa Céline | Drezet--Marçot | 400586 | enea.drezet-marcot@epfl.ch | `enea` |

The branch names intentionally contain only the surname, in lowercase and without accents.

---

## Project overview

This repository contains the group project for the Computational Carpentry module of CH-315.

The project is divided into three parts:

1. **Data structures and functions**
   - Load periodic-table data with `pandas`.
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

The final notebook must contain the code, results, explanations, and interpretations for every question.

---

## Repository contents

The repository should contain at least:

```text
.
├── GroupG_Block1_project.ipynb
├── periodic_table.csv
├── requirements.txt
├── README.md
└── .gitattributes
```

The structure may evolve during the project.

---

# 1. First-time setup for every collaborator

The steps in this section only need to be completed once on each computer.

## 1.1 Install the required software

Each collaborator needs:

- Git
- Anaconda or Miniconda
- VS Code Desktop
- the **Python** extension for VS Code
- the **Jupyter** extension for VS Code

Do not use `github.com` or `github.dev` to execute the notebook with the local Conda environment. Clone the repository and work from VS Code Desktop.

To verify that Git and Conda are installed, open a terminal and run:

```bash
git --version
conda --version
```

---

## 1.2 Clone the repository

Choose a folder on your computer where you want to store the project, open a terminal there, and run:

```bash
git clone https://github.com/eneadr/Modeling_Lab
cd Modeling_Lab
```

Do not download the project as a ZIP file if you intend to contribute. Cloning it with Git is necessary for branches, pulls, commits, and pushes.

---

## 1.3 Create the common Conda environment

All collaborators must use the same environment name and Python version.

Create the environment:

```bash
conda create -n mod_lab python=3.12 -y
```

Activate it:

```bash
conda activate mod_lab
```

Verify the Python version:

```bash
python --version
```

Verify which Python executable is being used:

```bash
python -c "import sys; print(sys.executable)"
```

On Windows, the path should normally contain something similar to:

```text
anaconda3\envs\mod_lab\python.exe
```

or:

```text
miniconda3\envs\mod_lab\python.exe
```

The exact beginning of the path depends on the computer and Windows username.

---

## 1.4 Install the project dependencies

Make sure `mod_lab` is activated:

```bash
conda activate mod_lab
```

Then install the packages listed in `requirements.txt`:

```bash
python -m pip install -r requirements.txt
```

A minimal `requirements.txt` for this project can contain:

```text
numpy
pandas
matplotlib
ipykernel
nbstripout
```

Add `scipy` only if the project actually imports it. For example, it is not required if reaction balancing is performed only with `numpy.linalg.svd`.

Whenever a new Python package becomes necessary for the project, add it to `requirements.txt` so that every collaborator can install the same dependency.

---

## 1.5 Register the Jupyter kernel

With `mod_lab` activated, run:

```bash
python -m ipykernel install --user --name mod_lab --display-name "Python (mod_lab)"
```

This registers the Conda environment as a Jupyter kernel.

Then open the project notebook in VS Code and select:

```text
Select Kernel
→ Select Another Kernel
→ Python Environments
→ Python (mod_lab)
```

Depending on the VS Code version, `mod_lab` may appear directly in the kernel list.

### If `mod_lab` does not appear

Press:

```text
Ctrl + Shift + P
```

Then select:

```text
Python: Select Interpreter
```

and choose the Python executable belonging to `mod_lab`.

On Windows, it will usually look similar to:

```text
C:\Users\<USERNAME>\anaconda3\envs\mod_lab\python.exe
```

or:

```text
C:\Users\<USERNAME>\miniconda3\envs\mod_lab\python.exe
```

Do **not** copy another team member's absolute Python path. Each collaborator has their own local installation path.

---

## 1.6 Verify the notebook environment

Run the following cell in the notebook:

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

The Python executable must point to the `mod_lab` environment.

If the imports work and the executable contains `mod_lab`, the environment is correctly configured.

---

# 2. Configure notebook cleaning for Git

Jupyter notebooks contain outputs, execution counts, kernel information, and other metadata. These can create Git differences even when the actual code has barely changed.

This repository uses `nbstripout` to remove unnecessary notebook outputs and metadata from the version committed to GitHub.

The notebook on the collaborator's computer can still contain outputs while they are working; the cleaning happens when Git stages the notebook.

## 2.1 Repository configuration

The repository should contain a `.gitattributes` file configured for `nbstripout`.


## 2.2 Configuration required on every collaborator's computer

After cloning the repository and activating `mod_lab`, every collaborator should run:

```bash
python -m pip install nbstripout
nbstripout --install
```

Then configure the additional metadata keys to remove:

```bash
git config filter.nbstripout.extrakeys "metadata.kernelspec metadata.language_info metadata.celltoolbar metadata.toc"
```

Check the configuration with:

```bash
nbstripout --status
```

This setup is local to each computer, so every collaborator must perform it once after cloning the repository.

---

# 3. Git branch organisation

The repository uses the following branches:

```text
main
├── marie
├── chloe
├── bertille
└── enea
```

### Branch ownership

- Marie Lacroix → `marie`
- Chloé Baruselli → `chloe`
- Bertille Delloye → `bertille`
- Enéa Drezet--Marçot → `enea`

`main` is the shared stable branch.

Each collaborator works on their own surname branch and sends completed work to `main` through a Pull Request.

### Important rules

- Do not work directly on `main`.
- Do not push unfinished work directly to `main`.
- Do not use `git push --force`.
- Pull the latest `main` before beginning new work.
- Keep commits small and understandable.
- Open a Pull Request before merging into `main`.
- Another team member should review the Pull Request when possible.
- Make sure the notebook runs before merging.

---

# 4. Create your personal branch for the first time

Each collaborator only creates their name branch if it does not already exist on GitHub.

Before creating it, update `main`:

```bash
git switch main
git pull --ff-only origin main
```

Then create the appropriate branch.

### Marie

```bash
git switch -c marie
git push -u origin marie
```

### Chloé

```bash
git switch -c chloe
git push -u origin chloe
```

### Bertille

```bash
git switch -c bertille
git push -u origin bertille
```

### Enéa

```bash
git switch -c enea
git push -u origin enea
```

The `-u` option connects the local branch to the corresponding branch on GitHub. After this first push, `git push` is sufficient.

Check the current branch at any time with:

```bash
git branch --show-current
```

---

# 5. Normal workflow before starting work

Every time you start a new working session, first update your local copy of `main`.

```bash
git switch main
git pull --ff-only origin main
```

Then switch to your personal branch:

```bash
git switch <name>
```

Before editing files, bring the latest `main` into your branch:

```bash
git merge main
```

If Git reports no conflicts, you can begin working.

The complete beginning-of-session workflow is therefore:

```bash
git switch main
git pull --ff-only origin main
git switch <surname>
git merge main
```

---

# 6. Save your work with Git

After making changes, first inspect them:

```bash
git status
```

Stage only the files you actually want to commit:

```bash
git add <modified-files>
```

For example:

```bash
git add GroupG_Block1_project.ipynb
```

or:

```bash
git add requirements.txt README.md
```

Then create a clear commit:

```bash
git commit -m "Implement molecular mass calculator"
```

Push the branch:

```bash
git push
```

If it is the first push of that branch, use:

```bash
git push -u origin <name>
```

---

# 7. Open a Pull Request

When a contribution is ready to be added to the stable project, open a Pull Request on GitHub.

On GitHub:

1. Open the repository.
2. Open **Pull requests**.
3. Click **New pull request** or **Compare & pull request**.
4. Set the base branch to `main`.
5. Set the compare branch to the collaborator's surname branch.
6. Give the Pull Request a clear title.
7. Briefly explain what was changed.
8. Mention how the work was tested.
9. Ask another team member to review it when possible.
10. Merge only when the notebook works correctly.

Example Pull Request description:

```text
Implemented the molecular-mass calculation section.

Changes:
- Loaded periodic_table.csv with pandas.
- Created the atomic-mass dictionary.
- Added the molecular_mass() function.
- Tested H2O, CO2 and C6H12O6.

The notebook runs without errors using the mod_lab kernel.
```

---

# 8. After a Pull Request is merged

After a contribution is merged into `main`, everyone should update their local `main` before continuing.

```bash
git switch main
git pull --ff-only origin main
```

The contributor should then update their personal branch as well:

```bash
git switch <name>
git merge main
git push
```
```

This keeps the personal branch synchronized with the latest stable version.

---

# 9. Avoiding conflicts in Jupyter notebooks

Branches help organise collaboration, but they do **not** automatically prevent `.ipynb` conflicts.

A Jupyter notebook is stored internally as a JSON document. Therefore, if two people edit the same notebook simultaneously, Git can report conflicts even if they modified different visible cells.

## Recommended rule

**Only one person should modify `GroupG_Block1_project.ipynb` at a time whenever possible.**

Before someone starts modifying the final notebook, the group should know who currently has responsibility for it.

For example:

```text
Marie edits the final notebook
→ Marie commits, pushes and merges
→ Chloé updates main
→ Chloé edits the next section
→ Chloé commits, pushes and merges
→ etc.
```

This sequential approach is the safest when everyone needs to contribute to the same notebook.

---

# 10. Recommended parallel workflow

If several team members need to work at the same time, avoid editing the final notebook simultaneously.

Instead, create separate temporary notebooks, for example:

```text
drafts/
├── lacroix.ipynb
├── baruselli.ipynb
├── delloye.ipynb
└── drezet.ipynb
```

Each person works only in their own draft notebook on their personal branch.

Once a section is finished and reviewed, its Markdown and code cells can be copied into:

```text
GroupG_Block1_project.ipynb
```

The person integrating the final notebook should first make sure their branch contains the latest version of `main`.

This approach is safer than four people modifying the same `.ipynb` file in parallel.

---

# 11. If `main` changes while you are working

If another Pull Request is merged while you are still working on your branch, update your branch before opening your own Pull Request.

First save or commit your current work.

Then run:

```bash
git fetch origin
git switch <name>
git merge origin/main
```

If there are no conflicts, test the notebook again and push:

```bash
git push
```

If there are conflicts, resolve them before continuing.

After resolving normal text-file conflicts:

```bash
git add <resolved-files>
git commit -m "Resolve merge conflict with main"
git push
```

For complicated notebook conflicts, do not manually edit the raw notebook JSON unless you understand its structure. A safer solution is usually to keep both notebook versions, open them in Jupyter or VS Code, and manually copy the correct cells into a clean notebook.

---

# 12. Updating dependencies

If a collaborator installs a new package needed by the project, for example:

```bash
python -m pip install scipy
```

that package must also be added to `requirements.txt`:

```text
scipy
```

Then commit the dependency change:

```bash
git add requirements.txt
git commit -m "Add scipy dependency"
git push
```

After the change is merged, the other collaborators update their environment with:

```bash
git switch main
git pull --ff-only origin main
conda activate mod_lab
python -m pip install -r requirements.txt
```

This prevents the situation where the notebook works on one computer but fails on another because a package is missing.

---

# 13. Reproducible random simulations

For Monte Carlo simulations, use a fixed random seed whenever reproducible results are required.

Example:

```python
import numpy as np

rng = np.random.default_rng(42)
```

Using the same seed allows all collaborators to reproduce the same pseudo-random results.

---

# 14. Useful Git commands

### Check your current branch

```bash
git branch --show-current
```

### See modified files

```bash
git status
```

### See local branches

```bash
git branch
```

### See local and remote branches

```bash
git branch -a
```

### Download information about remote changes without merging

```bash
git fetch origin
```

### Update `main`

```bash
git switch main
git pull --ff-only origin main
```

### Switch back to your personal branch

```bash
git switch <surname>
```

### Bring the latest `main` into your branch

```bash
git merge main
```

---

# 15. Daily Git checklist

## Before working

```bash
conda activate mod_lab

git switch main
git pull --ff-only origin main

git switch <surname>
git merge main

git status
```

Confirm that you are on your own surname branch before editing files.

## After working

```bash
git status
git add <modified-files>
git commit -m "Clear description of the work"
git push
```

When the contribution is complete, open a Pull Request from the surname branch into `main`.

---

# 16. Final checklist before opening a Pull Request

Before opening a Pull Request, verify that:

- you are working on your surname branch and not on `main`;
- your branch contains the latest relevant changes from `main`;
- the notebook opens correctly;
- the `Python (mod_lab)` kernel is selected;
- all cells required for your contribution run without errors;
- required data files are present;
- any new dependency has been added to `requirements.txt`;
- `git status` does not show accidental or unrelated files;
- notebook metadata/output cleaning is active;
- your commit message clearly describes the change.

---

# 17. Final project checks before submission

Before submitting the project:

1. Make sure all accepted Pull Requests have been merged into `main`.
2. Update the local `main` branch:

```bash
git switch main
git pull --ff-only origin main
```

3. Activate the project environment:

```bash
conda activate mod_lab
```

4. Select `Python (mod_lab)` as the notebook kernel.
5. Restart the kernel.
6. Run the final notebook from the first cell to the last cell.
7. Check that no cell produces an unexpected error.
8. Check that figures, tables, numerical results, explanations, and interpretations are present.
9. Check that the final notebook is named correctly:

```text
GroupG_Block1_project.ipynb
```

10. Confirm that the version on GitHub is the same version that will be submitted.

---

# Summary of the collaboration workflow

```text
1. Clone repository
2. Create and activate mod_lab
3. Install requirements.txt
4. Register Python (mod_lab)
5. Configure nbstripout
6. Update main
7. Switch to your surname branch
8. Merge the latest main into your branch
9. Work and test
10. Commit
11. Push
12. Open a Pull Request into main
13. Review and merge
14. Everyone pulls the new main
15. Repeat
```

The most important rules are:

- `main` must remain the stable shared version.
- Each collaborator works on their surname branch.
- Do not edit the final notebook simultaneously unless absolutely necessary.
- Pull the latest `main` before starting new work.
- Test before merging.
- Keep `requirements.txt` synchronized with the packages actually used by the project.
- Keep unnecessary notebook outputs and metadata out of Git with `nbstripout`.
