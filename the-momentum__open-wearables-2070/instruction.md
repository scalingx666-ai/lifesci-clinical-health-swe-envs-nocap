# Issue

**Title:** feat: add the previous_day_activity health score category

## Description

## What does this change?

Adds the health score category `previous_day_activity`. The frontend knows it as "Previous day activity" and the docs list it.

## Why?

Some activity scores can only be calculated once the day they describe is over, so they are recorded on the next day while representing the previous one. Stored as `activity`, a client would show such a score as the same "Activity" as one that describes the day it is recorded on (e.g. Oura's), so the two would sit side by side under one name but cover different days. A category of its own keeps them apart.

## How did you test this?

Backend and frontend tests for the new category (filtering by it, its place in the frontend's category order), the full backend suite, lint and the OpenAPI export check.

## AI usage

Claude Code was used to review the changes

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Added a “Previous day activity” score category, displayed separately from same-day activity scores.
  * Previous-day activity scores are recorded the following day and appear in their own category.
* **Documentation**
  * Updated health score references to include the new category.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7ca121dd4e48`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.