# Issue

**Title:** fix: improve PyPI release workflow

## Description

## Summary
- Add `release: [created]` trigger so builds run when releases are created on github.com
- Add `contents: write` permission to fix "Resource not accessible by integration" error on release upload
- Fix PEP 440 compliance for manual test build versions (`0.0.0.devYYYYMMDDHHMMSS`)
- Replace custom release notes generation (~150 lines) with GitHub's built-in `generate_release_notes`

## Test plan
- [x] Manual workflow_dispatch test on TestPyPI passed
- [x] Tag push (1.0.5) verified: PyPI upload, TestPyPI upload, and Release asset upload all succeeded
- [x] Release v1.0.5 confirmed with both `.whl` and `.tar.gz` assets attached

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fa343335cf83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.