# Issue

**Title:** Update Maven plugins

## Description

This should be a safe maintenance update that does not affect functionality.

- [dicoogle][sdk] Update maven plugins
   - maven-compiler-plugin 3.11.0
   - maven-shade-plugin 3.5.1
   - maven-resources-plugin 3.3.1
   - frontend-maven-plugin 1.14.0
      - update nodeVersion to 18.17.1 and npmVersion to 9.6.7
   - license-maven-plugin 4.3
   - formatter-maven-plugin 2.16.0
      - This is the only plugin I could not update to the latest version, because we want to continue supporting Java 8
- Format Java code
- Reorganize .gitignore
   - Add `/target`, remove obsolete lines, rearrange lines

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0a514aac7115`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.