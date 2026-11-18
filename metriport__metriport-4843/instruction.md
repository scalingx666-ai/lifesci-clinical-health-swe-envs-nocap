# Issue

**Title:** ENG-1224: support row data field in payload on backend

## Description

### Dependencies

- Downstream: 

### Description

This allows us to cleanly pass the data from a given row to the backend for inference. It's backwards compatible.

### Testing

Tested against api on my machine

### Release Plan

- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Medical inference responses now include a structured preface summarizing resource type, displays, and core data.
  * Requests can supply optional additional resource data, which is incorporated and shown in the generated response.
  * Assistant outputs provide expanded, multi-line context ahead of the main message for clearer interpretation.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e367e736fdba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.