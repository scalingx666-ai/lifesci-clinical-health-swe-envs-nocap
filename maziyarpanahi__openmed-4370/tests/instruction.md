# Issue

**Title:** Fix source-span alignment in escaped HTML output

## Description

## Description

HTML output currently escapes the source before applying entity offsets, so an ampersand or angle bracket can move the highlight onto the wrong text or split an HTML character reference. Map source boundaries into escaped text before adding highlight tags, while retaining the existing escaping protection from #403.

## Type of Change

- [x] Bug fix
- [x] Test improvement

## Changes Made

- Preserve source text and entity offsets while rendering escaped HTML.
- Handle adjacent and nested ranges without inserting tags into escaped characters; ignore invalid ranges for rendering.
- Add one data-driven regression in the existing processing suite and record the fix in the 3.2.0 changelog.

## Testing

- [x] Processing suite: 53 passed and 12 passing subtests, including hostile metadata, special characters, Unicode, nested/adjacent spans and invalid ranges.
- [x] The new regression fails on the original candidate and passes with this fix.
- [x] Full combined v3.2 rehearsal: 24,224 passed, 158 skipped and 11,344 passing subtests; canonical formatting/lint, scoped hooks, strict documentation, package validation and SDK readiness pass.
- [x] The complete prepared branch tree matches the reviewed rehearsal step. Final hosted platform checks run on #4369 after integration.

## Documentation

- [x] Updated CHANGELOG.md.

## Code Quality

- [x] Ran `make format`, `make lint` and `make format-check` on the combined candidate.
- [x] Reviewed the source-coordinate mapping and escaping behavior.

## Dependencies

- [x] No new dependencies or dependency pins.

## Related Issues

. Targets `prepare/v3.2.0` for inclusion in #4369.

## Example

For `A & B: Alice`, an entity at the source span for `Alice` highlights exactly `Alice`; the ampersand remains escaped and the source offsets stay unchanged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d721cbe117d2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.