# Issue

**Title:** perf(search): Read each _include target once

## Description

`getSearchIncludeEntries` passed one reference per base resource to `readReferences`, so many resources sharing a target (e.g. 1000 Slots related to 40 Schedules) charged FHIR quota, logged a read AuditEvent, and queried the database once per reference.

Dedupe references before reading reduces the overhead of these operations without impacting the returned results.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cc4822d14333`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.