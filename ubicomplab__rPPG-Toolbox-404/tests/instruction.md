# Issue

**Title:** Update PhysFormerTrainer.py

## Description

Bug in `train` function in `PhysFormerTrainer`. The `get_hr` function is used in line 105 to get the ground truth Heart Rate using the ground truth ppg signal. This function uses the `sr` variable for sampling rate. This should be set according to the frame rate of the ground truth ppg. Currently, it is set to a fixed value of `30 Hz` and this is used for all datasets leading to incorrect heart rates.  Modified line 105 to use the correct sampling or frame rate each time: 
`get_hr(i, sr=self.frame_rate)`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `40c1a68bcc33`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.