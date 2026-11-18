# Issue

**Title:** Fix relative reference resolution within bundles

## Description

Fixes relative reference resolution for references within a bundle by moving the server reference from abstract resource model to the abstract base model, and walking up the owner hierarchy directly rather than using `owningResource` to walk up the chain of domain resources (which doesn't include `Bundle`).

Also renames the `server` property to `origin_server` to reduce potential name conflicts with FHIR resources.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4455e0b0001d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.