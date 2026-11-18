# Issue

**Title:** [ENH] Add options for output and build folder

## Description

Not ready. 
Needs replication in windows. 

Added functionality allows to easily generate different build/ and out/ folders. 

```build_project.bat Debug_testA``` will pour bins (in -g mode) into ```build/Debug_testA``` folder and output into ```out/Debug_testA``` folder (also in Debug mode). As long as there is an input argument which not being ```coverage, clean, mock or help```, has a "Debug" included in it.

```build_project.bat Release--testB``` will generate use ```build/Release--testB``` and output binary files to ```out/Release--testB``` all in release mode. As long as there is an input argument which not being ```coverage, clean, mock or help```, has a "Release" included in it.

```build_project.bat Debug_testA clean``` or ```build_project.bat clean Debug_testA``` will generate clean builds.

```build_project.bat Debug_testA clean mock``` or ```build_project.bat mock Debug_testA clean``` or ```build_project.bat Debug_testA mock clean``` will show you the commands without actually executing them. 

Easy(er) to change and compare build configurations.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `069740de80fa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.