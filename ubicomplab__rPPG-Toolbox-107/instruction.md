# Issue

**Title:** resolving issue w/ os specific separator

## Description

addressing issue `Native Windows UBFC Testing gives an Error due to path splitting in DataLoader #106`
Changed os specific path separator in BaseLoader.py to os.sep. 

Confirmed proper function by running: 

python main --config_file PURE_PURE_UBFC_TSCAN_BASIC.yaml

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c8e311e2d3e2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.