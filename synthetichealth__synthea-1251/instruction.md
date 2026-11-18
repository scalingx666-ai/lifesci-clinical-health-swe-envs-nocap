# Issue

**Title:** Update CI action versions

## Description

Update the versions of the actions used in our CI to address some of the deprecation warnings. 

For example see https://github.com/synthetichealth/synthea/actions/runs/4117160673  
If you dig into the log https://github.com/synthetichealth/synthea/actions/runs/4117160673/jobs/7108119437  you can see that the deprecation warnings come from the steps "Set up JDK" and "Gradle cache".

The only difference beyond just version numbers is we now need to specify a java distribution to use:
https://github.com/actions/setup-java/blob/main/docs/switching-to-v2.md  
`'zulu'` was the implicit default previously so I stuck with that here.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a1affc363488`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.