# Issue

**Title:** 8476 Allow NOPs for unchanged resources with auto-versioned references

## Description

Resubmitting an unchanged resource with an auto-versioned reference in a transaction always created a new version, because the deferred auto-versioning pass forced a version bump on every resource. The deferred resources are now saved targets-first (see `AutoVersionSaveOrder`): the target of an auto-versioned reference is saved before the resource referencing it, so the target can be a NOP and the resource referencing it gets the target's actual version. Forcing a new version is left for reference cycles only, where a target has to be saved after a resource that already references its expected (incremented) version.

Also correct the resolved ID in TransactionDetails after each save, so an auto-versioned inline match URL reference to a NOP target gets the real version rather than the expected incremented one.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `06dd3f57cda7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.