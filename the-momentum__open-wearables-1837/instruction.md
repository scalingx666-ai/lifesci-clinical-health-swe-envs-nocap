# Issue

**Title:** chore: add CodeRabbit labeling instructions

## Description

## What does this change?

Adds `labeling_instructions` to `.coderabbit.yaml` with the labels that make sense on PRs (area, provider, `breaking-change`) and when to apply each one.

## Why?

After enabling `auto_apply_labels` in #1799, CodeRabbit didn't apply anything on #1800, even though it flagged the breaking change in its review. Without `labeling_instructions` it only learns from labels on previous PRs, and most of ours have none. Issue-only labels like `draft` or `provider-request` are left out so they don't end up on PRs.

## How did you test this?

Checked that every label in the list exists on GitHub. Whether CodeRabbit picks the right ones will show on the next PRs.

## AI usage

Claude Code helped write the labeling instructions.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Chores**
  * Added automated pull request labeling rules based on the areas and types of changes.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2851c0c09039`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.