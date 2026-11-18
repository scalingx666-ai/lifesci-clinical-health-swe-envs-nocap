# Issue

**Title:** Fix: Prevent crash on cross-sectional data in get_correlation_matrix and update np.nan

## Description

## Description
This PR fixes two crashes that occur when a user attempts to compute a correlation matrix or plot thrivelines using cross-sectional data (such as the `fcon1000` dataset used in the tutorials).

### Motivation and Context
Currently, if a user runs `model.compute_correlation_matrix(train)`  on purely cross-sectional data, the algorithm attempts to merge subjects across different ages. Since there are no overlapping `subject_ids`, it creates an empty array. This eventually gets passed to scikit-learn's `LinearRegression.fit()`, which triggers a cryptic crash: `ValueError: Found array with 0 sample(s)`. 

Additionally, the code used `np.NaN`, which was permanently removed in NumPy 2.0, causing an immediate `AttributeError` on newer Python environments.

### Changes Made
* **Added a boundary check:** Inserted a check at the beginning of `get_correlation_matrix` in `pcntoolkit/math_functions/thrive.py`. If the data lacks longitudinal measurements (no duplicated `subject_ids`), it now raises a clear, descriptive `ValueError` explaining that longitudinal data is required.
* **NumPy 2.0 Compatibility:** Replaced the outdated `np.NaN` with `np.nan` in `thrive.py`.



<img width="995" height="479" alt="image" src="https://github.com/user-attachments/assets/79dc2324-a455-46e7-b768-ba854c85b75a" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `497068927978`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.