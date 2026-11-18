# Issue

**Title:** translate: export the device vocabulary bundle

## Description

## Offline device vocabulary export

`mirobody device-bundle [--out PATH]` writes a deterministic JSON bundle with catalogue metrics, labels, LOINC device crosswalks, vendor fields, unmappable entries, version stamps and a SHA-256 digest. Phone clients can consume the same vocabulary as the server.

Updated against the 1.5.2 main branch. The label loader now reads `res/catalog/labels/` after the catalogue move. Verified the CLI output equals the module output byte for byte (316 metrics, 13 vendors, 340,836 bytes), and its digest verifies; Ruff, compileall and six import contracts pass. Current GitHub checks are shown in the PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a2a7ac69d52e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.