# Issue

**Title:** Use $PY_BINARY  to install PIP on Debian-based systems. Closes zatosource/zato#955

## Description

When installing Zato from sources on a Debian-based system, the PIP package should be python-pip when working on Pyhton 2.7 and python3-pip when using Python 3. This is accomplished by using the existing variable $PY_BINARY to build the package name.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fd7246bbb752`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.