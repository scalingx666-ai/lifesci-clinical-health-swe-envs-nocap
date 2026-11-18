# Issue

**Title:** ci: drop deleted utils.permissions from release import gate

## Description

Second (and last) blocker for the 1.2.1 release: the wheel bare-import gate imported `mirobody.utils.permissions`, deleted as dead code this PR, so it raised ModuleNotFoundError and Publish was skipped. Now imports `mirobody.utils` alone. Both bare-install gates reproduced green locally against the built wheel in a clean 3.12 venv. PyPI still 1.0.62; re-tagging 1.2.1 after merge will publish.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1ea511600cb6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.