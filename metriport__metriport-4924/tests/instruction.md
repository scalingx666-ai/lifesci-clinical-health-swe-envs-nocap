# Issue

**Title:** feat(ihe): remove catpure on PD

## Description

Ref: ENG-000

### Description

- we no longer send failures to PG... this alert is meaningless https://metriport-inc.sentry.io/issues/5125422091/?environment=production&query=&referrer=issue-stream&statsPeriod=30d

### Testing

- Local
  - [ ] N/A
- Staging
  - [x] run PD
- Sandbox
  - [ ] N/A
- Production
  - [ ] run PD

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Changes**
  * Removed in-app notifications about incomplete gateway results during polling operations. System monitoring continues with internal logging.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2b85d851fe6d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.