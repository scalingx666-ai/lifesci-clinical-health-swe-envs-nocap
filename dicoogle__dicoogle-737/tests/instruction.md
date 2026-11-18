# Issue

**Title:** Rename server setting archive/support-wsi to archive/use-iio-registry

## Description

This resolves the concern raised  while keeping it compatible with existing instances still using the other name.

- Rename `support-wsi` to `use-iio-registry` and document setting in getter at server settings reader
- keep `support-wsi` as an alias
- add test coverage for setting this property via alias

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `44481367388c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.