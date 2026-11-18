# Issue

**Title:** Reorganize a little bit: add ./docs, ./demos, and MAINTAINERS.md

## Description

- Move all the docs config into ./docs
- Move all the flask app files into ./demos/flask
- Move the maintainer-specific instructions from README.md into MAINTAINERS.md so that we don't bore people

This supercedes #71

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `64fe3f697cf6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.