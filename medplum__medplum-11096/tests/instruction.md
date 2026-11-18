# Issue

**Title:** fix(server): add project write constraints for project admin synthetic access policy

## Description

Add a write constraint to the project admin access policy entries for User and ProjectMembership: a new resource's project element, if present, must be the admin's own Project. Updates are unchanged, since project is already a read-only field.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `05e81b5b7938`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.