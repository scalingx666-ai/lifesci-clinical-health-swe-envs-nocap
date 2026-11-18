# Issue

**Title:** feat(react): client-free LabListItemView and LabResultListItemView

## Description

Adds LabListItemView and LabResultListItemView: client-free row bodies that take resolved resources as props, for partners calling the Medplum API directly. LabListItem and LabResultListItem keep their props and wrap the views with useResource and MedplumLink.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `97a4e8ef932c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.