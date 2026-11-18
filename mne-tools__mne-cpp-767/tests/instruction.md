# Issue

**Title:** [ENH] Link scaling

## Description

This update solves some thing that have been not working properly for some time regarding the scaling controls. 
The scaling sliders worked reversed (left = higher amplitude) and sometimes the graph was glitchy.
This solves these issues. Internally the methods to process the callback for each scaling control update (double spinboxes or sliders) and are now independent. 
I've implemented a link (by default) between MAGs and GRADs channel amplitudes. Which can be set by pressing the SHIFT key. 
I've also done a bit of cleaning.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1671412fda90`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.