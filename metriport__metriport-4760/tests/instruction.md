# Issue

**Title:** ENG-954 Remove DB cluster init sql

## Description

Ref eng-954



### Dependencies

- Upstream: 
- Downstream: none

### Description

Remove DB cluster init sql  - [context1](https://github.com/metriport/metriport/actions/runs/18063971652/job/51404197538), [context2](https://metriport.slack.com/archives/C094AJ8L0E8/p1759003150212929?thread_ts=1758906123.315339&cid=C094AJ8L0E8)

### Testing

none

### Release Plan

- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* New Features
  * Removed automatic setup of the analytics database schema and S3 integration during deploys/updates.
* Bug Fixes
  * Removed automated wait-and-apply behavior that handled schema creation to prevent deployment race conditions.
  * Reverted explicit target-schema enforcement for the incremental FHIR-to-CSV pipeline.
* Chores
  * Tuned deployment timeouts to enhance stability during database initialization.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c2367a2cef4e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.