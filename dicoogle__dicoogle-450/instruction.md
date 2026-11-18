# Issue

**Title:** Fix exportToCSV modal on webapp

## Description

This PR fixes the Export to CSV modal issues.
The button styles were changed and now match the web app style. Mobile version is considered.
The input field to name the export preset was also fixed and the user can now change the name.

Before:
![Screenshot 2021-02-16 at 12 41 48](https://user-images.githubusercontent.com/8323694/108064293-5e80df80-7054-11eb-8556-eb8c7a121f06.png)

Now:
![now](https://user-images.githubusercontent.com/8323694/108063889-cd116d80-7053-11eb-8d8a-99e2c5e6c452.png)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9bf18f5a9ce9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.