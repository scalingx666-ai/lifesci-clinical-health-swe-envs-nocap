# Issue

**Title:** ci: disable CodeRabbit auto reviews

## Description

**Problem:** CodeRabbit reviews every PR on its own, which adds noise.

**Solution:** Set `reviews.auto_review.enabled: false` in `.coderabbit.yml`. The now unused `ignore_title_keywords` list is removed. Reviews still run on request with `@coderabbitai review`.

**Steps to reproduce**
1. Open a PR against `develop`.
2. Before: CodeRabbit posts a review on its own. After: it does not, until someone comments `@coderabbitai review`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `676813027fee`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.