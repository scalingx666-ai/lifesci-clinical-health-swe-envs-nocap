# Issue

**Title:** Qualify language support with explicit abstention and graduation gates

## Description

## Description

Keep language and dialect routing conservative, define explicit low-resource graduation requirements, and stabilize the public readiness report. Additional synthetic evidence remains separate from model-backed support and native clinical review.

## Included pull requests

- #4269 — deterministic offline language/dialect abstention, retaining the measured recommendation to keep the deterministic route.
- #4291 — initial experimental cohort with independent recall, native-review, packaging and cross-language regression gates.
- #4316 — incremental path/version and Markdown readiness contract on top of the runtime already merged through #3617.

## Issues resolved

## Maintainer changes

- Update all sources from current master and preserve their contributor history and documentation.
- Refuse zero-byte model package evidence and inventory all six explicit augmentation-only generators independently of bundled model routes.
- Keep selection-time fixture counts conservative, every cohort locale experimental and native-review roles unfilled.
- Clarify that public BLAKE2 personalization is not a secret key and keep short/unstable input handling conservative.
- Verify existing issue discussions by exact ID, date, author and body. No new model adoption or clinical-validation claim.
- No cross-PR runtime fixes: the real combined tree matches the complete passing rehearsal.

## Validation

- 207 focused checks and `make format`, `make lint`, `make format-check` passed.
- Complete rehearsal: 23,965 tests passed, 155 skipped, 11,220 subtests passed (273.73s).
- Strict docs and three protected Chromium checks passed: asset budgets, one homepage analytics beacon and clinical-page exclusion.
- Wheel/sdist build and all three changed package-module byte checks passed. Wheel 8,038,400 bytes within the unchanged 8,633,884-byte budget.
- Exact final SHA `7c20125194373974e52ecab22c3af287b34bf8a3` passed every gate again: 23,965 tests, 155 skips, 11,220 subtests (238.18s) and 207 focused checks. The final wheel is byte-identical to rehearsal.

## Documentation and dependencies

Updated language, graduation and readiness guides, navigation/publication metadata, golden Markdown and Unreleased notes. No new dependencies. Inventory and synthetic controls do not prove model quality or clinical validation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b72a2d51a416`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.