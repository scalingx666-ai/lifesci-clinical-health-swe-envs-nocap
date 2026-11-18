# Issue

**Title:** Correct SNR calculation to reflect reference

## Description

This PR makes some corrections to the SNR calculation in order to properly reflect the approach used in the CHROM paper, and as mentioned in the bottom of page six of [this paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7899506/pdf/boe-12-1-494.pdf).

Using the `PURE_UBFC-rPPG_TSCAN_BASIC.yaml` for testing, here's results (including SNR) prior to corrections:

FFT MAE (FFT Label): 1.2974330357142858 +/- 0.3951013616658031
FFT RMSE (FFT Label): 2.8704957923240366 +/- 3.0489809798112115
FFT MAPE (FFT Label): 1.500155568072648 +/- 0.4672290826823667
FFT Pearson (FFT Label): 0.9890524988652464 +/- 0.02333192795742126
FFT SNR (FFT Label): 1.4945164762235956 +/- 1.1317032218020173 (dB)

And results after corrections:

FFT MAE (FFT Label): 1.2974330357142858 +/- 0.3951013616658031
FFT RMSE (FFT Label): 2.8704957923240366 +/- 3.0489809798112115
FFT MAPE (FFT Label): 1.500155568072648 +/- 0.4672290826823667
FFT Pearson (FFT Label): 0.9890524988652464 +/- 0.02333192795742126
FFT SNR (FFT Label): 6.641024545844431 +/- 1.1291389587742173 (dB)

This does seem to have a significant effect on the SNR, so I propose in a future iteration of the arXiv that all supplementary results that include SNR should be updated.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cf0c09419b94`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.