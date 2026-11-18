# Issue

**Title:** Keep Lucene indexes written before the Lucene 9.12 upgrade readable

## Description

## For Code Reviewer

Lucene 9.12 made `Lucene912` the default codec and moved the previous one, `Lucene99`, out of `lucene-core` into `lucene-backward-codecs` (apache/lucene#13585). Since the move to Hibernate Search 8.2 / Lucene 9.12, a JPA server with an existing on-disk Lucene index fails to open it with `Could not load codec 'Lucene99'`.

The test opens a zip file index because it has to be one written by the older Lucene (9.11.1).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6d818eaa401f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.