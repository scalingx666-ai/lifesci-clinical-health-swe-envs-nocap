# Issue

**Title:** [Fix] Memory leak in MNE library in bem related functions

## Description

In ```add_bem_surface``` there seems to be a leak of ```newSurf``` 

In ```add_replace_display_surface``` I'm not sure about ```surf``` variable. @LorenzE do you remember about this function?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6937d76549af`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.