# Issue

**Title:** RhythmFormer and PhysMamba fixes

## Description

The following changes were made as a result of an investigation of issue #368:

* Some code for logging and saving plots for learning rate and loss information, as well as saving model outputs, was missing from `RhythmFormerTrainer.py`. This has been fixed alongside some minor changes to the corresponding config files to remove an erroneous `AUG` parameter and add in some missing parameters. 
* For one PhysMamba config file, the log path was different from every other config file. This has been corrected.
* For some RhythmFormer and PhysMamba config files, Bland-Altman Plot generation has been enabled by default just like the other configs.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0e43e93147d7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.