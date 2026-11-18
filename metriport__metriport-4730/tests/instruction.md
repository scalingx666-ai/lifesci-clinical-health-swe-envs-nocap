# Issue

**Title:** feat(utils): improve FF test file

## Description

Ref: ENG-000

Issues:

- https://linear.app/metriport/issue/ENG-000

### Dependencies

- none

### Description

Improve dev experience by tweaking the FF file and providing an example of how to use FFs test so it does not affect bundles locally. This will bring visiblity to what needs to be reverted. 

### Testing


- Local
  - none
- Staging
  - none
- Sandbox
  - none
- Production
  - none

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

- Documentation
  - Clarified guidance for configuring DYNAMODB_ENDPOINT when using a local DynamoDB instance.
- Tests
  - Adjusted test payloads to remove an active feature-flag insertion and replaced it with commented placeholders to better mirror real scenarios.
- Note
  - No runtime or user-facing behavior changes.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aab4396ecfb7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.