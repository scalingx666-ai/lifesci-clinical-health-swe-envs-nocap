# Issue

**Title:** Support Physnet

## Description

Result(Train on 80%PURE, validate on 20%PURE and test on UBFC):

FFT MAE (Peak Label):29.38613250059878
Peak MAE (Peak Label):9.25217675206949
FFT MAE (FFT Label):28.982642389112904
Peak MAE (FFT Label):10.733994715369535
FFT RMSE:35.32016268894528
PEAK RMSE:13.697248274185613
FFT RMSE (Peak Label):34.219600622081174
PEAK RMSE (Peak Label):11.705877256184394
FFT RMSE (FFT Label):35.103693409025155
PEAK RMSE (FFT Label):14.291589947137457
FFT MAPE:27.41744236745305
PEAK MAPE:10.850602331058798
FFT MAPE (Peak Label):27.558608430196262
PEAK MAPE (Peak Label):9.296338784538507
FFT MAPE (FFT Label):26.75027412108773
PEAK MAPE (FFT Label):11.176562904949716
FFT Pearson:0.009937353355856141
PEAK Pearson:0.7635945637934934
FFT Pearson (Peak Label):0.03557894529361652                                                          
PEAK Pearson  (Peak Label):0.799496395233178
FFT Pearson (FFT Label):-0.0023980959903129847
PEAK Pearson (FFT Label):0.7557810078839305

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ba4b3c65ced7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.