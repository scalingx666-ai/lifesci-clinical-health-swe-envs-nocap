# Issue

**Title:** OBLS-1075 Fix UI defect with backorder reference column

## Description

Before:
<img width="1763" height="569" alt="image" src="https://github.com/user-attachments/assets/b3a73b62-8ff6-4be1-b371-03eb8fcc9e26" />

After:
<img width="1864" height="479" alt="image" src="https://github.com/user-attachments/assets/31671fc4-2328-4c2d-9285-99530b944614" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fe0e8b875a8c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.