# Issue

**Title:** Pseudo ppg label function

## Description

**Train: PURE, Test: UBFC-rPPG, Model: TSCAN**
FFT MAE (FFT Label): 1.3392857142857142 +/- 0.42190125596543704
FFT RMSE (FFT Label): 3.044620560179667 +/- 3.5261431285376057
FFT MAPE (FFT Label): 1.5575960591866085 +/- 0.5049767631839935
FFT Pearson (FFT Label): 0.988079459671649 +/- 0.02434079978913088

**Train: PURE Pseudo Labels, Test: UBFC-rPPG GT Labels, Model: TSCAN**
FFT MAE (FFT Label): 9.375 +/- 2.5283082691165326
FFT RMSE (FFT Label): 18.87773870342228 +/- 142.48195440534639
FFT MAPE (FFT Label): 13.307904748480684 +/- 4.077642607327307
FFT Pearson (FFT Label): 0.582888550823001 +/- 0.12847576982834757
FFT SNR (FFT Label): -1.8506740608244514 +/- 1.7017036801128422

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0bd1a1702732`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.