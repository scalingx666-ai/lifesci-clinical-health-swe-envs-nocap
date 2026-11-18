# Issue

**Title:** enh: compute BLR yhat in one pass

## Description

Part of #576 (row 2a). Based on `dev`. It does not need #572 or #577.

## What it does

`compute_yhat` computes the predicted mean (Yhat). The generic version in `RegressionModel` averages over 200 Z values and calls `backward()` once for each. Each call builds the design matrix again and solves with the posterior precision matrix `A` again, with the same result every time.

The new `BLR.compute_yhat`:
1. computes the predictive mean and variance once;
2. maps all 200 Z values in one array operation;
3. if the model has a warp, applies the inverse warp to the whole array in one call.

The transfer corrections (the mean and scale per batch effect) were copied in 3 places. They are now in one helper, `BLR.predictive_ys_s2`, which `forward`, `backward`, `elemwise_logp` and `compute_yhat` all use.

No API change. The default behaviour is the same.

## Results

Yhat is **bit-identical** to the old code. I checked:
- the saved plain, hetero, warp, hetero_be and multi-variable reference models from #572;
- a transferred model (Z, centiles, logp and Yhat);
- the FCON and synthetic cases in the table below.

## Speed

`NormativeModel.predict`, 8-core laptop, best of 3:

| Data | Model | N | R | Before | After | Speed-up | Yhat identical |
|---|---|---|---|---|---|---|---|
| FCON1000 | hetero | 325 | 5 | 0.380 s | 0.068 s | 5.6× | yes |
| synthetic | plain | 10 000 | 10 | 3.46 s | 0.34 s | 10.2× | yes |
| synthetic | warp | 10 000 | 10 | 5.41 s | 0.70 s | 7.7× | yes |

On the small #572 reference models (N=100), `compute_yhat` alone is about 100× faster (35 ms → 0.4 ms).

## Validation

I checked and timed this PR with the benchmark and validation code in #572. This PR does not include that code.

## AI use

Claude Opus 5.5 (Claude Code) wrote the code and this description, and ran the benchmarks and the equivalence checks. A human set the rules in #576 and reviews this PR.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Mr7sVWVWnqWZUEYkYUaeLy

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e5d45baef758`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.