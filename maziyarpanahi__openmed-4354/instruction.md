# Issue

**Title:** Integrate native GLiNER tasks and language qualification

## Description

Expose typed native GLiNER2 tasks and fixed-option decisions, with a pinned offline qualification report for language routing. The scalar-level repair refuses unrepresentable requests before inference. The evaluation preserves deterministic routing and language-pack defaults.

## Included pull requests

- #4273 — Typed GLiNER2 entities/classification/relations/schema extraction, six checkpoint capability records and the native decision backend.
- #4283 — Pinned multilingual language/script/dialect/code-switch evaluation and value-free report.

## Maintainer integration changes

Repairs remain on their owning originals: native scalar levels now return unsupported instead of a false success; the current Sinhala corpus has a model-facing codebook; the report/docs were regenerated from actual cached CPU inference. Inspected stacked-history conflicts affect only documentation and changelog; the real tree equals the passing rehearsal exactly.

The  retains deterministic abstention. The prior 462-sample receipt remains historical evidence.

## Validation

Complete rehearsal 29ed17463b077f4baf3b309ceb83305bcb4a40fe: 23,332 passed, 155 skipped, 11,220 subtests passed; 96 focused controls passed, 3 opt-in checks skipped. Canonical tooling, strict docs, three browser guards, all four package payload checks and the 7,919,413-byte wheel budget passed. A frozen clean-core install proved lazy optional loading, the missing-runtime hint and a 6,270µs import against 300,000µs.

Real proof: fastino/GLiNER2.5-multi-Decide@e173bca1f0c4217d7a55b3b0c705d5ece8a0218d, CPU, 514 synthetic decisions with every socket blocked; Spanish public-API decision passed. The existing published offline integration reproduced the report in 46.83s. Small-checkpoint entity inference was not run locally. Model weights are not bundled; the measurements do not establish clinical qualification.

Final exact-head gates passed on 67b8f1c392c028ec6577717823a19593fc9d500f: 23,332 tests/11,220 subtests passed, 155 skipped; canonical tooling, strict docs, all three browser guards and package checks passed. Its wheel is byte-for-byte identical to the clean-core-tested rehearsal. Hosted SDK, security, lint and image gates passed; Linux test lanes were still running with no observed failures.

## Issues resolved

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `29cfcf4b3aa3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.