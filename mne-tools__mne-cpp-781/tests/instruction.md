# Issue

**Title:** [ENH] Add no plugin configure options

## Description

It is now possible to disable plugins in MNE Scan, MNE Analyse and MNE Rt Server:

- To disable MNE Scan plugins run: qmake MNECPP_CONFIG+=noMneScanPlugins
- To disable MNE Analyze plugins run: qmake MNECPP_CONFIG+=noMneAnalyzePlugins
- To disable MNE Rt Server plugins run: qmake MNECPP_CONFIG+=noMneRtServerPlugins

One potential use case for this is to create separate CI workflows, as proposed by @gabrielbmotta and @juangpc.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bd280ca4234b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.