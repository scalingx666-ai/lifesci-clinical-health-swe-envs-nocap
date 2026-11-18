# Issue

**Title:** feat: assemble cited ambient note drafts

## Description

## Description
Ambient notes need evidence that survives source revisions, redaction and speaker review. Add a local composition and finalization pipeline that only sends freshly PHI-screened, finalized, role-reviewed transcript evidence to the note extractor. Each statement retains original-offset citations, extraction provenance and uncertainty.

Uncited, contradicted, unsupported or conflicting statements remain blocked. Finalization reruns screening and verification, checks unchanged source/role bindings, and resolves exact clinician review through trusted local custody before returning a protected local note. It never updates a medical record.

.

## Type of Change
- [x] New feature
- [x] Documentation update
- [x] Test addition/improvement

## Changes Made
- Compose the existing role-review and PHI-withholding gates, preserving original ledger coordinates through actual redaction mappings.
- Screen generated statements before returning them or invoking verification; retain a hold if generated PHI required redaction.
- Validate bounded sections, statement identities, complete extraction steps, exact request/model bindings and non-overlapping citations.
- Verify actual cited text with its reviewed speaker alias and role. Add an adapter for an explicitly supplied local OpenMed NLI backend; select no default model or cloud fallback.
- Reuse deterministic claim-conflict review for assertion disagreement and hold conflicting declared values, unresolved scope and uncertainty.
- Bind review to the complete note, evidence, policy and model context through ReviewedLocalEvidence. Reject stale, changed, expired, revoked or unavailable clinician custody, including changes during callbacks.
- Add the public guide, runnable synthetic example, navigation/publication registration and changelog entry.

Provider declarations are contracts, not sandboxes or model qualification. Applications must qualify their local models and enforce authenticated clinician permission in the trusted review authority. The heuristic NLI example is synthetic demonstration only. Note text remains protected; public audit serialization excludes source and generated text.

## Testing
- [x] Focused tests: **53 passed**.
- [x] Full suite on the final source: **24,727 passed, 158 skipped, 11,361 subtests passed** (88 warnings; 250.72 seconds).
- [x] Canonical `make format`, `make lint`, `make format-check`, `make type-check`, `make brand-check`.
- [x] Explicit mypy on the new module, public API compatibility and classified-effect inventory.
- [x] Strict MkDocs build: **155.13 seconds**; final runnable example passed.
- [x] Scoped pre-commit, Bandit, secret detection and diff whitespace checks.
- [x] Incoming attribution policy: all seven commits against master and the single feature commit against the prerequisite merge.
- [ ] Hosted checks pending on this PR's exact head.

Tests exercise real withholding and local NLI paths, Unicode citation mapping, clipped identifiers, output PHI, stale or incomplete responses, contradictory claims, uncertainty, revoked review, source changes during callbacks, expiry, limits and value-free offline reports.

## Documentation and Dependencies
- [x] Added docstrings and `docs/multimodal/streaming/ambient-note-evidence.md`.
- [x] Updated changelog, navigation and publication inventory.
- [x] No new third-party dependencies.

This branch contains latest master `29ffa70050cc7729a0051be419a1b090699a5ed1` and preserves the prerequisite commits from #4386, #4388, #4392 and #4400. The base remains master so full CI runs. Merge those prerequisites first; the issue-specific change is `9828189bffdbcd860de33b970d9b93437846b3a9` (six files). The cumulative diff includes those still-open prerequisites.

## Example
A screened statement such as “The patient reports cough.” retains its original transcript offsets and reviewed speaker attribution. An uncited claim, negation conflict, changed screen result or revoked clinician receipt cannot finalize the earlier draft.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `84ad829ab6f3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.