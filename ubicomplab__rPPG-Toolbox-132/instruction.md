# Issue

**Title:** Clean-up main.py and small fix in baseloader

## Description

As the title states. I've tested this PR using the inference config file UBFC_PURE_TSCAN_BASIC.yaml. I was able to 1) run inference successfully using existing preprocessed data folders, 2) preprocess PURE all over again with DO_PREPROCESS set to True and run inference successfully on it, and 3) run inference successfully using the newly created preprocessed data folder, with DO_PREPROCESS set to False. I got the same result below every time:

===Testing===                                                                                                                                                                                  
Testing uses pretrained model!                                                                                                                                                                 
                                                                                                                                                                                               
FFT MAE (FFT Label):3.694385593220339                                                                                                                                                          
FFT RMSE (FFT Label):13.848831292145585                                                                                                                                                        
FFT MAPE (FFT Label):3.3882176381266618                                                                                                                                                        
FFT Pearson (FFT Label):0.8176110623563922 

Also note the following for the test set length as reference:
test Preprocessed Dataset Length: 647

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f2a3a5cc5862`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.