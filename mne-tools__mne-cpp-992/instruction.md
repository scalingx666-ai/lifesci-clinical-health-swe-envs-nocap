# Issue

**Title:** Remove codeql for staging

## Description

Looking at https://github.com/mne-tools/mne-cpp/actions/workflows/codeql.yml I see 9 runners in the last 2h that will each be tied up for about an hour

<img width="1198" height="713" alt="Screenshot 2026-05-01 at 10 21 02 AM" src="https://github.com/user-attachments/assets/ba60bd9b-36a9-48a6-9245-dde2395b9cfe" />

This PR aims to reduce this usage by just running CodeQL on `main`. I am not sure what the dev workflow is here exactly, but assuming you merge stuff from `staging` to `main` occassionally then this would help with the concurrency issues.

Feel free to close and fix a different way, but it would be good to get something like this in ASAP so that other repo workflows can continue!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `59a509990960`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.