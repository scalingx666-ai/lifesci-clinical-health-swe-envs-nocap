# Issue

**Title:** Support PhysDrive Dataset

## Description

PhysDrive, the first large-scale multimodal dataset for contactless in-vehicle physiological sensing with dedicated consideration on various modality settings and driving factors. PhysDrive collects data from 48 drivers, including synchronized RGB, near-infrared camera, and raw mmWave radar data, accompanied with six synchronized ground truths (ECG, BVP, Respiration, HR, RR, and SpO2). 
See more on https://www.kaggle.com/datasets/xiaoyang274/physdrive

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f0889de2b383`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.