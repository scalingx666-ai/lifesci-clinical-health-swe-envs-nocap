# Issue

**Title:** Preserve CJK date formats during date shifting

## Description

## Description

Chinese/Japanese `年/月/日` and Korean `년/월/일` dates can be masked or converted into ISO text during date shifting even though the locale parser recognizes them. Shift recognized dates with that parser and render the numeric components back into their original format.

## Type of Change

- [x] Bug fix
- [x] Test improvement

## Changes Made

- Preserve date markers, spacing, component widths and source digit systems, with or without python-dateutil.
- Retain keep-year handling and fail-closed masking for invalid dates, overflow and ambiguous two-digit-year century changes.
- Extend the existing date-shift suite with three data-driven checks, including public pipeline paths, and add the 3.2.0 changelog entry.

## Testing

- [x] Date-shift suite: 267 passed and 40 passing subtests, covering zh/ja/ko, full-width digits, leap dates, rollover, keep-year behavior and negative cases.
- [x] The new regressions fail on the original candidate and pass with this fix.
- [x] Full combined v3.2 rehearsal: 24,224 passed, 158 skipped and 11,344 passing subtests; canonical formatting/lint, scoped hooks, strict documentation, package validation and SDK readiness pass.
- [x] The complete prepared branch tree matches the reviewed rehearsal step. Final hosted platform checks run on #4369 after integration.

## Documentation

- [x] Updated CHANGELOG.md.

## Code Quality

- [x] Ran `make format`, `make lint` and `make format-check` on the combined candidate.
- [x] Reviewed date parsing and fail-closed behavior.

## Dependencies

- [x] No new dependencies or dependency pins.

## Related Issues

. Targets `prepare/v3.2.0` for inclusion in #4369.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `508a36ce9d20`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.