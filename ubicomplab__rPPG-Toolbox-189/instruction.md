# Issue

**Title:** Fix bug with variables in sample window code

## Description

Some quick, post-fix results:

[Without smaller sampling window]
FFT MAE (FFT Label): 1.1172537076271187 +/- 0.7542595904048776
FFT RMSE (FFT Label): 5.900322033631117 +/- 33.75286796464523
FFT MAPE (FFT Label): 1.2770134322717948 +/- 0.8337279906070219
FFT Pearson (FFT Label): 0.9689888394596143 +/- 0.03272978926468511
FFT SNR (FFT Label): 8.942749400609268 +/- 0.9383277604051053 (dB)

[With smaller sampling window of 30 seconds]
FFT MAE (FFT Label): 0.7683153973509934 +/- 0.22184007908928535
FFT RMSE (FFT Label): 2.832220802488396 +/- 3.953023632536723
FFT MAPE (FFT Label): 1.0609250742855765 +/- 0.32449846005783045
FFT Pearson (FFT Label): 0.992227258511806 +/- 0.010194440999366668
FFT SNR (FFT Label): 8.8876280935758 +/- 0.6228435207812865 (dB)

[With smaller sampling window of 60 seconds]
FFT MAE (FFT Label): 1.1272927989130435 +/- 0.5379340392718027
FFT RMSE (FFT Label): 5.28139260710191 +/- 22.183051361442022
FFT MAPE (FFT Label): 1.58381447066447 +/- 0.6952154803215566
FFT Pearson (FFT Label): 0.9731489451139645 +/- 0.024262712732727697
FFT SNR (FFT Label): 7.540904400822264 +/- 0.7572398223976812 (dB)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c8862a59bc4d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.