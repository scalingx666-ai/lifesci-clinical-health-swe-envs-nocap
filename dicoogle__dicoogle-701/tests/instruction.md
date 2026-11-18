# Issue

**Title:** Additional Methods for Index/Unindex Operations in Platform Interface

## Description

Implemented 1 index method for >1 URIs and several unindex methods for the platform interface.

We can now use the platform interface to dispatch unindex tasks for singular URIs or batches, which is performed and handled by `PluginController`. The new index method allows dispatching tasks for batches of URIs.

A minor code refactoring was performed in a few files, and `indexBlocking` was marked as deprecated, as requested by @Enet4

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `390ab782fe83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.