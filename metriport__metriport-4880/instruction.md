# Issue

**Title:** ENG-1297: fix resource summary prompt

## Description

### Dependencies

None

### Description

New refactor may have restructured the prompt and somehow broken the styling.

### Testing

Ran the prompt against a bunch of resources and conditions

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Style**
  * AI-generated answers now formatted with structured bullet-pointed sections for improved readability.

* **Refactor**
  * Streamlined prompt instructions by consolidating guidance into inline instructions for clearer, more consistent response generation.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `402f73593aa8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.