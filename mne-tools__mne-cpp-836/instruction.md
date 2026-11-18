# Issue

**Title:** [ENH,Fix] Solve occasional crashing of MNE Scan

## Description

I observed occasional crashes of MNE Scan after the first successful fit. Specifically, the crash happened while the computed dev_head_trans was applied to the scaled and transformed average head. It seems that the issue was that the applied transformation was not affine, meaning that the last row was not (0,0,0,1). Qt only applies affine transformations and therefore errored sometimes. 

![image](https://user-images.githubusercontent.com/40984141/132952261-7f2ee4ed-5b45-4c3c-b611-a6a4719d5b7c.png)

Since we should only apply affine transformations anyway, I implemented a new convenience function to set a new transformation of an existing FiffCoordTrans. This function enforces affine transformations automatically. The function also avoids working on members directly, which shouldn't be done in the first place as well, I guess. 

Note: one some point one could try to clean up the casting mess between double and float matrices

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `635bb87b77bc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.