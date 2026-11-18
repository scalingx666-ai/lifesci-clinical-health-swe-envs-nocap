# Issue

**Title:** Dev pymc coords

## Description

Refactored the HBR method to utilize arviz coords. This creates named dimensions, and makes the code a bit cleaner. 
https://cluhmann.github.io/inferencedata/
https://oriolabrilpla.cat/en/blog/posts/2020/pymc3-arviz.html

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9ef1df1a2854`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.