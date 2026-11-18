# Issue

**Title:** Ensure server settings support for multiple providers

## Description

Although what we had before was less verbose, it wasn't working quite well for multiple providers due to some implementation quirks in Jackson (#342). So, this PR changes both DIM provider and default storage listings to be wrapped around XML elements, making the intent of supporting multiple providers clearer.

- wrap server settings XML elems `dim-provider` with `dim-providers`
- wrap server settings XML elems `default-storage` with `default-storages`
- update Jackson XML dependencies
- add respective tests

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0e19fda7cac1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.