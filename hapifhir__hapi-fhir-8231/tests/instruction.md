# Issue

**Title:** Fix same-partition Patient $merge blocked by compartment enforcement

## Description

Fixes

### The problem

In Patient ID partitioning mode, a Patient `$merge` failed with HTTP 412 / `HAPI-2476` when the source and
target Patients resolved to the **same** partition id and a patient-compartment resource referenced the
source.

The rejection comes from **`PatientCompartmentEnforcingInterceptor`**, which blocks any update that would
move a resource out of the patient compartment it was stored under. It and the merge asked different
questions:

- **The enforcer** compares the whole `RequestPartitionId`. `PatientIdPartitionInterceptor` puts the patient
  id part in the partition *name*, so the enforcer correctly sees the compartment would change, and throws
  `Msg.code(2476)`.
- **The merge** compared only the numeric partition id. Two patient ids can hash to the same partition, and
  when they do it found no difference — so it concluded the resource did not need to move and updated it in
  place, which is exactly the write the enforcer rejects.

### The fix

- `ResourceMergeService` (routing) and `PartitionAwareReplaceReferencesSvc` (per-resource classification)
  now compare the full `RequestPartitionId`, recomputed from resource content — the same question the
  enforcer asks.
- That computation moved to `IRequestPartitionHelperSvc`, and `PatientCompartmentEnforcingInterceptor` was
  refactored onto it, so the two cannot drift apart.

A compartment resource whose compartment changes is therefore **moved** rather than updated in place, even
when both patients hash to the same partition, and undo restores it under its original id.

### Tests

`PatientIdModePatientMergeR4Test.SamePartitionMergeWithCompartmentEnforcement` uses two patient ids that
collide onto one partition. It fails on the base branch and passes here.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5fa1ff6d3b2c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.