# Issue

**Title:** Pure data split fix

## Description

Added get_data_subset helper function to PURE data loader. This interfaces with the get_data function. The PURE data loader now ensures thats there is no subject overlap between data splits (train/val/test). The helper function may be used to improve other dataloaders that have multiple trials per individual (eg. COHFACE). 

The function of this change was tested with the following command:
$python main.py --config_file ../configs/PURE_PURE_UBFC_TSCAN_BASIC.yaml

It should also be noted that preprocessing was enabled for both PURE train and validation sets. 
The final portion of the train/test output can be seen below:

====Training Epoch: 9====
Train epoch 9:  77%|███████████▌   | 99/129 [00:44<00:11,  2.61it/s, loss=0.559][10,   100] loss: 0.655
Train epoch 9: 100%|██████████████| 129/129 [00:55<00:00,  2.31it/s, loss=0.612]
===Validating===
Validation: 100%|████████████████████| 34/34 [00:09<00:00,  3.51it/s, loss=0.43]
Saved Model Path:  PreTrainedModels/PURE_SizeW72_SizeH72_ClipLength180_DataTypeNormalized_Standardized_LabelTypeNormalized_Large_boxTrue_Large_size1.5_Dyamic_DetFalse_det_len180/PURE_PURE_UBFC_tscan_Epoch9.pth
validation loss:  0.6434635905658498
best trained epoch:5, min_val_loss:0.6389700279516333
===Testing===
Testing uses non-pretrained model!
PreTrainedModels/PURE_SizeW72_SizeH72_ClipLength180_DataTypeNormalized_Standardized_LabelTypeNormalized_Large_boxTrue_Large_size1.5_Dyamic_DetFalse_det_len180/PURE_PURE_UBFC_tscan_Epoch5.pth
FFT MAE (FFT Label):1.5667459239130435
FFT RMSE (FFT Label):3.2319068072410806
FFT MAPE (FFT Label):1.9091061076627633
FFT Pearson (FFT Label):0.9909906631057575

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8c02ca4c01c6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.