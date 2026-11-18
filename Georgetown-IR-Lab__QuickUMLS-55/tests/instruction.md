# Issue

**Title:** QuickUMLS v.1.4

## Description

- [NEW] Added support for [unqlite](https://github.com/coleifer/unqlite-python) as an alternative to leveldb for storage of CUIs and Semantic Types. This allows creating multiple QuickUMLS matchers with from the same installation.
- [NEW] added support for conversion of all uppercase words (, thank you sandertan@!).
- [NEW] Automatically downloads SpaCy data for selected language if missing.
- [FIX] Mitigated .

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bd58713e8172`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.