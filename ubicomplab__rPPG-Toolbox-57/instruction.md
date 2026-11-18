# Issue

**Title:** Multi process new

## Description

1support multi_process; support pure and ubfc right now.
(fix a problem about loading ubfc data comparing with the last PR)
2.fix the divide 0 problem when executing the differential function in preprocessing
3.modify test metric output: output the fft mae when testing the one performing badly.

The results using PURE_PURE_UBFC_TSCAN_BASIC.yaml:
best trained epoch:9, min_val_loss:0.6025826158848676
FFT MAE:3.7471527303225813
Peak MAE:2.42235114522146
FFT MAE (Peak Label):4.11204899958862
Peak MAE (Peak Label):1.2500307408909053
FFT MAE (FFT Label):0.87890625
Peak MAE (FFT Label):4.770518009428924
FFT RMSE:5.350771983900685
PEAK RMSE:4.0136881527100545
FFT RMSE (Peak Label):5.815684213582905
PEAK RMSE (Peak Label):2.0489723279128738
FFT RMSE (FFT Label):1.9652941208494246
PEAK RMSE (FFT Label):6.24516021897639
FFT MAPE:3.811077222160765
PEAK MAPE:2.7261595558278655
FFT MAPE (Peak Label):4.214562942382564
PEAK MAPE (Peak Label):1.3376022280992559
FFT MAPE (FFT Label):1.0687431302735944
PEAK MAPE (FFT Label):5.078192763265566
FFT Pearson:0.964428555314126
PEAK Pearson:0.9795677325060552
FFT Pearson (Peak Label):0.9608331599862353
PEAK Pearson (Peak Label):0.9940894551250475
FFT Pearson (FFT Label):0.9959239573665501
PEAK Pearson (FFT Label):0.9508937289180358

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ba4b3c65ced7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.