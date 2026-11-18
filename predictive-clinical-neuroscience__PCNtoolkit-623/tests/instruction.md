# Issue

**Title:** fix: score compare_hbr_models on the fit data

## Description

#### AI assistance

I used Claude Code

#### Reference issue (if any)

#### What does this implement/fix?

Option (a) of #620: `compare_hbr_models(models, data)`.

1. The function takes `data`, the `NormData` the models were fitted on. For each model and response variable it preprocesses a copy of `data` with the model's scalers, compiles a fresh PyMC model with `likelihood.compile(X, be, be_maps, Y)`, and calls `pm.compute_log_likelihood` with the saved posterior (`HBR.idata`). Nothing is synthesized: the result no longer depends on NumPy's global random state, and neither the loaded models nor `data` are modified.
2. It compares only the response variables that are in `data` and in every model, and warns about the others. It raises `TypeError` if a model is not an HBR, and `ValueError` if no model can be loaded, if no response variable is left, if `data` is not compatible with a model, or if the models do not transform and scale the response variable identically (log likelihoods on different scales are not comparable). The last check applies each model's `y_transform` and outscaler to `data` and accepts differences up to 1e-9, so rounding differences between outscalers fitted on the same data pass.
3. It warns when a model was fitted with `advi`, `pathfinder` or `laplace` (question 3 of #620). The check also accepts the `InferenceMethod` objects of #597.
4. Tutorial 07 (`examples/07_model_comparison.ipynb`): the call becomes `compare_hbr_models(dct, train)`. The notebook is re-executed, and its RST page and downloadable copy are regenerated with `doc/convert_notebooks.py`. Model2 now ranks clearly first for WM-hypointensities (elpd_diff -90, dse 13), and the two models cannot be told apart for Right-Lateral-Ventricle.
5. New `test/test_util/test_model_comparison.py` (11 tests): the log likelihood equals the one computed with the PyMC model built at fit time (rtol 1e-10); a model whose noise SD is far too small is ranked last; the result is the same for two states of the global generator; `data` is not modified; outscalers that differ by one unit in the last place are accepted; models with a doubled SD or a mean shifted by 1e-6 SD are rejected; response variables missing from `data` or from a model are skipped with a warning, and a `ValueError` is raised when none is left; a BLR model is rejected; a model marked `advi` triggers the warning.

Breaking change: `compare_hbr_models(dct)` now raises `TypeError` (missing `data`). The only caller in the repository is tutorial 07.

Not included: a Jacobian term to compare models fitted on different scales, and a held-out comparison (option d of #620).

#### To reproduce

The script of #620, with `compare_hbr_models(paths, train)` in part 1. Output on this branch (progress bars removed; part 1 is rounded by `az.compare`'s default `round_to="auto"`):

```
true noise SD on the standardised scale: about 0.79

1. compare_hbr_models(paths, train) with this PR, three states of NumPy's global generator
            rank     elpd      p  elpd_diff     dse  weight
free           0   -150.0    3.5        0.0     0.0    0.92
too_narrow     1 -15000.0  616.0   -15000.0  2000.0    0.08

            rank     elpd      p  elpd_diff     dse  weight
free           0   -150.0    3.5        0.0     0.0    0.92
too_narrow     1 -15000.0  616.0   -15000.0  2000.0    0.08

            rank     elpd      p  elpd_diff     dse  weight
free           0   -150.0    3.5        0.0     0.0    0.92
too_narrow     1 -15000.0  616.0   -15000.0  2000.0    0.08

2. PSIS-LOO on the 120 training subjects, same saved posterior samples
            rank     elpd      p  elpd_diff     dse  weight
free           0   -145.2    3.5        0.0     0.0     0.9
too_narrow     1 -14682.5  616.0   -14537.3  1963.1     0.1
```

Part 1 now gives the reference of part 2, for all three states of the generator.

Tests run locally (related modules only, as asked in `AGENTS.md`): `test/test_util/test_model_comparison.py`, `test/test_regression_models/test_hbr.py` and `test/test_util/test_migration.py`, 49 passed. `ruff format` and `ruff check` add no finding on the changed files.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6e516024aaf1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.