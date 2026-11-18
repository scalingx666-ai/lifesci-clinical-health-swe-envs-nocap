# Issue

**Title:** Fix broken Dokka API Doc links on brand new website

## Description

for #2232

This will fix the currently broken links on https://google.github.io/android-fhir/use/api/.

It also automagically makes sure that they will never break again in the future by enabling link validation.

@MJ1998 LGTY?

@fredhersch FYI

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a7ae30961241`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.