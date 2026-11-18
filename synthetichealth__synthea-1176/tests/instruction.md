# Issue

**Title:** Modify RIF tests so there are always DME claims.

## Description

Modify RIF tests so there are always DME claims.

- Adds a hearing aid module for only the unit tests.
- Adds a mock DME mapper class to ensure the hearing aid claim is exported regardless of the presence of mapping files.
- Ignore sonatype-lift complaints about "God Classes" -- we hear you, now go away.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8a2e87dcb629`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.