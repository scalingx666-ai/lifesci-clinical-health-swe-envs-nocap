# Issue

**Title:** RELEASE ENG-1297: Use recursive summarization to prevent breaking context window

## Description

### Dependencies

None

### Description

- 
- 

### Testing

Check each PR.

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

## Release Notes

* **New Features**
  * Added Groq SDK integration for enhanced LLM capabilities
  * Introduced token usage tracking and metrics reporting for medical record summarization
  * Added utilities for text chunking and byte formatting

* **Improvements**
  * Enhanced prompt handling with template-driven workflow for medical inference
  * Improved CSV value escaping for special characters

* **Tests**
  * Added test coverage for byte formatting and text chunking utilities

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cbc1f1e589c7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.