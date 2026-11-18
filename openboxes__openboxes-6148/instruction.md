# Issue

**Title:** OBLS-955 Properly display negative inventory on the product's stock card

## Description

https://openboxes.atlassian.net/browse/OBLS-955

<img width="1899" height="874" alt="image" src="https://github.com/user-attachments/assets/ab235998-2b01-40b4-b2d3-24b90b0da02c" />


FYI: If there is someone out of the loop looking into this PR, negative stock on a specific bin is allowed in VVG project (if configured properly)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e2aeaf0842d1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.