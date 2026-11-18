# Issue

**Title:** Internal valid

## Description

This branch is improved with the option of internal validation. So train dataset and validation dataset can be from a single dataset but have different parts of it. You need to set the beginning and ending of the dataset in the yaml. For example, BEGIN:0.0 END :1.0 means the whole dataset; BEGIN:0.0, END:0.5, you will get first half of it.

run it with PURE_PURE_UBFC_TSCAN_BASIC.yaml, and you will get:
validation loss:  0.6062100800600919
Best epoch: 9
Peak MAE (Peak Label):1.9202421352969026
FFT MAE (FFT Label):0.7938508064516129
PEAK RMSE (Peak Label):3.214203744439965
FFT RMSE (FFT Label):2.175897866546737
PEAK MAPE (Peak Label):2.0814058265504083
FFT MAPE (FFT Label):0.9667061138734013
PEAK Pearson  (Peak Label):0.9814270164261616
FFT Pearson (FFT Label):0.9945183994331132

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8228610b0153`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.