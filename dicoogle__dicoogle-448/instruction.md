# Issue

**Title:** WebUI Plugins: Fix the emit events for result-batch slot plugins

## Description

Currently, the result-batch plugins are not able to receive the list of (patients,studies, series, images) to apply actions. 
Actually it fails before to try to emit the proper values. There are two fixes:
- Webcore: allow to emit signals 
- Patient,Study.. Images: properly get a list of images, was probably failing due to dependency updates such as react, react-bootstrap and all these related matters.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fbaff9b77678`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.