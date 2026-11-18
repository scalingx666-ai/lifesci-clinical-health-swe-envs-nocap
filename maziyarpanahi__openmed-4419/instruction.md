# Issue

**Title:** feat: connect the offline multimodal reference workflow

## Description

## Description
Connect the multimodal components in one offline synthetic reference workflow. It takes a generated PNG and WAV through bounded preflight and decoding, actual pixel redaction, local fixture-provider inference, transcript PHI withholding, visual evidence fusion, clock alignment, unknown-speaker review and owned-buffer cleanup.

The normal result remains `review_required`, with `complete: false` and `clinical_write_allowed: false`. Interrupted or degraded runs cannot produce a successful review handoff. Cleanup failures discard the handoff; external and immutable copies remain explicitly outside the owned-buffer destruction guarantee.

## Type of change
- [x] New feature
- [x] Documentation and integration tests

## Changes
- Add source-checkout orchestration, generated fixtures, an executable example and a guide.
- Bind visual claims to original coordinates and the actual redaction receipt; retain original transcript token timing and redaction mappings.
- Propagate conflicting visual readings and unknown speaker roles into review without fabricating a note or clinician approval.
- Exercise cancellation at every stage, malformed/truncated assets, unresolved PHI, memory/thermal pressure before and after inference, provider exceptions, deadline expiry and cleanup failures.
- Keep the default explicitly synthetic: the WAV is a tone and providers verify actual fixture inputs before replaying known controls. These controls do not measure model accuracy or clinical privacy recall.

## Dependencies and review scope
Built from current master `29ffa7005`, preserving the prerequisite histories from #4418, #4417, #4416, #4405, #4414 and #4398. The new reference implementation is commit `730b67f99`. The combined lockfile preserves both existing optional native-runtime extras; this feature adds no new dependency.

## Validation
- Full Python suite: **26,976 passed, 158 skipped, 11,380 subtests passed**.
- Reference integration controls: **33 passed** on Python 3.12 and in the frozen Python 3.11 development environment.
- Combined OpenMedKit suite: **187 tests, 17 skipped, zero failures**.
- Canonical formatting, lint, type checks, explicit module mypy, public API compatibility, effect inventory and scoped pre-commit passed.
- Strict documentation build and exact Pages artifact validation passed; executable example passed.
- Wheel and sdist built, Twine passed, and both contain the exact tested source.
- Frozen development and combined native-runtime dependency audits passed.
- Both unchanged real native-provider profiles passed in the combined environment using existing local assets under OS network denial. This is separate from synthetic reference replay, not joint clinical validation.
- Complete incoming commit-attribution check passed for all 81 commits.

## Documentation
- [x] Guide, navigation, publication metadata and changelog updated.
- [x] New public entry points documented.

## Example
`python -m examples.multimodal.ambient_reference` prints content-free source and cleanup receipts with:
```json
{
  "status": "review_required",
  "reached_review": true,
  "complete": false,
  "clinical_write_allowed": false,
  "all_data_erased": false
}
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1bd524377b8a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.