# Issue

**Title:** [MAINT] Update BrainStat Version

## Description

This PR tackles 
- Updating dependencies. _Note_ :
Upgrading BrainStat implies to downgrade on NetNeurotools : 
```bash 
 - Downgrading netneurotools (0.3.0 -> 0.2.5)
 - Updating brainstat (0.4.2 -> 0.5.2)
 ```
- Drop python 3.9, adapt to python 3.13 (replacement for #1510)
- Removing an unused function `remove_dummy_dimension`
- Moving around parts of the code to follow standards

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0c1591645129`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.