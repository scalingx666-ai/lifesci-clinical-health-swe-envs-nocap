# Issue

**Title:** Remove - 1 term from RGB normalization

## Description

This - 1 term doesn't change any of the current results and was pretty harmless to begin with since all it did was shift the normalized RGB distribution to be centered around 0, but to stay true to the original algorithm and as discussed in #139 I think it should be removed.

Result before removal:

FFT MAE (FFT Label):5.772477489406779
FFT RMSE (FFT Label):14.925515271353694
FFT MAPE (FFT Label):11.5169233509023
FFT Pearson  (FFT Label):0.809478372260371

Result after removal:

FFT MAE (FFT Label):5.772477489406779
FFT RMSE (FFT Label):14.925515271353694
FFT MAPE (FFT Label):11.5169233509023
FFT Pearson  (FFT Label):0.809478372260371

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b483b40217ed`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.