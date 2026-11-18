# Issue

**Title:** fix: handle missing scatter_data in plot_centiles_advanced

## Description

## Fix: handle missing `scatter_data` in `plot_centiles_advanced`

 

### Problem

`plot_centiles_advanced` crashes when called without `scatter_data` in two scenarios:

1. **Saving plots**: `plotname` is only defined inside `if scatter_data:`, but the `save_dir` logic at the end uses it unconditionally → `NameError`
2. **Multi-covariate models**: The midpoint computation for non-plotted covariates accesses `scatter_data.X` unconditionally → `AttributeError`

### Changes

Minimal two-line fix in `plotter.py`:

1. **Default `plotname`**: Added  
   `plotname = f"centiles_{response_var}"`  
   before the `if scatter_data:` block so it always has a value when saving.

2. **Covariate fallback**: When `scatter_data` is `None`, the non-plotted covariate value now falls back to the midpoint of the model's stored covariate range instead of trying to compute the mean from scatter data.

### Verification

After the fix, the following calls work without error:

```python
# Save centile-only plot
plot_centiles_advanced(model, save_dir="./plots")

# Multi-covariate model without scatter data  
plot_centiles_advanced(multi_cov_model)
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e09154b32b8d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.