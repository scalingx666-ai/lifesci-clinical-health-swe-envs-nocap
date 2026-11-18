# Issue

**Title:** Small improvements in button UI for search result slot.

## Description

Small improvements in button UI for search result slot.

Before:

![Screen Shot 2021-02-07 at 17 22 06](https://user-images.githubusercontent.com/110873/107154110-0a497180-6969-11eb-80d1-7dd1b7d3ef89.png)

After: 

![slots-image](https://user-images.githubusercontent.com/110873/107154054-bdfe3180-6968-11eb-9452-7bb52ed16d78.png)

The plugins that interects with search results are currently totally broken, but hopefully can submit a patch soon.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f7a0eba0d0e8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.