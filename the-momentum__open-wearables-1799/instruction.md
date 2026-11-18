# Issue

**Title:** chore: let CodeRabbit apply PR labels automatically

## Description

## What does this change?

CodeRabbit now applies the labels it picks for a PR instead of only suggesting them in the review summary.

## Why?

We label issues fairly consistently but often forget on PRs, especially the provider labels and `breaking-change`. CodeRabbit already chooses from the labels we have on GitHub, so we don't need to list them in the config.

## How did you test this?

Not tested yet. It only kicks in once CodeRabbit reviews a PR with this config. I'll check the labels on this PR and the next few.

## AI usage

Claude Code helped find the config option.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Chores**
  * Review items are now labeled automatically. This is an internal workflow update and does not change the product experience.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `73dd4437e31d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.