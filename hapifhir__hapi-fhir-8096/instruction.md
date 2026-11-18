# Issue

**Title:** Reduce id-sequence lock contention under high write concurrency (opt-in per-thread pooling)

## Description

Under high write concurrency, database id generation could bottleneck because all writer threads on a server shared a single id pool guarded by one lock, held across the nextval() round-trip during pool refills.

  This adds an option to allocate ids from a per-thread pool instead, so concurrent writers each draw from their own block and never serialize on that lock.

  Behavior / compatibility
  - Disabled by default — existing deployments are unaffected on upgrade. Enabled via JpaStorageSettings#setPerThreadIdSequencePoolingEnabled(true).
  - The two optimizers interpret the same DB sequence value differently, so per-thread pooling must be enabled cluster-wide in one coordinated restart, never node-by-node (documented in upgrade.md).
  - When enabled, ids are no longer handed out in strict creation order across threads. The package installer's "most recent existing version" selection now sorts by _lastUpdated (with internal id only as a tiebreaker) instead of by internal id.

  Tests
  - New HapiSequenceStyleGeneratorTest — guards optimizer selection and the reserved-value (HAPI-2791) guard.
  - ResetSequencesTestHelper handles both optimizers.
  - Retained the server-assigned reserved-value integration test in DeletedDatabaseRowsR5Test.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0a0bbcf3aed7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.