# Issue

**Title:** feat: gate ECG measurements on acquisition quality

## Description

## Description
ECG interval processing must not continue silently through missing samples, clipping, flatlines, noisy/drifting signals or unverified acquisition calibration. Add deterministic per-lead quality assessment and a guarded measurement callback with explicit, versioned thresholds.

**Prerequisite: #4387 (lead identity/layout).** This branch contains that prerequisite plus one separate implementation commit. It targets master so the complete CI matrix runs. Merge #4387 first, then refresh and revalidate this PR; the cumulative prerequisite diff will disappear once it lands. Latest master `29ffa70050cc7729a0051be419a1b090699a5ed1` is included.

## Type of change
- [x] New feature
- [x] Documentation and focused regression controls

## Changes
- Measure missing fraction, contiguous gaps, declared-rail clipping, bounded-range flatlines, block-median baseline change, local second-difference roughness and calibration gain error.
- Assign pass, limited-use, review or reacquire states using explicit policy bounds. Missing evidence and insufficient proxy coverage cannot become a pass; no good metric compensates for a failed required gate.
- Reassess original lead layout, sample count, timing and full-record calibration coverage. Bind source, actual normalized samples, acquisition declaration and policy using digests.
- Reassess quality before every measurement invocation, require explicit reviewer confirmation, and pass only required leads to the callback. Sanitize callback failures and exclude protected values from diagnostics.
- Document proxy limitations and a runnable synthetic example; register the guide in navigation and the publication manifest.

The scores are acquisition indicators, not a diagnosis or clinical qualification. No recommended clinical thresholds, ECG measurement algorithm, Swift acquisition pipeline or automatic clinical action is introduced. Application callbacks remain responsible for their own privacy and side effects.

## Testing
Validated implementation head: `c02b50ff7ec3dde9db69bfda6d4975df0a3ade54`.

- 65 focused signal-quality tests; 152 combined ECG tests.
- Full suite: **24,653 passed, 158 skipped, 11,361 subtests passed**.
- Publication contract: 52 passed, 25 subtests passed after adding the guide manifest entry.
- `make format`, `make lint`, `make format-check`, `make type-check`, `make brand-check`.
- Explicit mypy for the new module; public API compatibility check.
- Strict MkDocs build and executable guide example.
- Scoped pre-commit, Bandit, secret checks and complete commit-attribution checks against master and the prerequisite.

Controls include injected noise bursts, drift, clipping, gaps and flatlines; all-missing input; stale evidence; changed calibration; split calibration coverage; threshold boundaries; optional-lead exclusion; blocked callback non-invocation; and protected error/repr output.

## Documentation and dependencies
- [x] Guide, public docstrings and changelog updated.
- [x] Self-review complete; focused implementation commit.
- [x] No new dependencies.

## Example
A required lead with a corrupted segment produces a blocked quality report and the measurement callback is never called. An otherwise acceptable waveform with absent gain/rail evidence remains in review. Synthetic input meeting its explicit policy can reach the callback only after reviewer confirmation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cd172a295c4b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.