# Issue

**Title:** fix(api): suspects propmt

## Description

### Dependencies

- Downstream: 

### Description

Add prompting for suspecting

### Testing

Tested against api on my machine

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

- **New Features**
  - Added support for the “Suspects” resource type with three auto-generated questions: “Why was this suspect created?”, “What are the related resources responsible for this suspect?”, and “Other key observations related to this suspect?”; Suspects data is now included in generated patient summaries.

- **Style**
  - Improved prompt and output formatting to preserve structure and integrate Suspects context cleanly into final summaries.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a4d47582200`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.