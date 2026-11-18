# Issue

**Title:** Support tag expiry in instance and facility tag configs

## Description

## Proposed Changes

Adds frontend support for tag expiry from ohcnetwork/care#3792 (backend branch `ENG-737-backup`, which the Playwright CI job already runs against). Tag configs at the instance level (`/admin/tag_config`) and facility level (facility settings) share the same form and details page, so both get the same changes.

- **Tag config form:** a new Expiry section built with CareUI `FieldSet`, `Field`, `Switch`, `Input` and `FieldError`:
  - "Expire automatically" with a days/hours/minutes offset, which must be above zero when on.
  - "Allow changing expiry", which lets users pick their own expiry when applying the tag.
  - Sends `expiry_metadata`; turning both switches off clears it.
- **Tag config details:** shows the rule, e.g. "Removed 7 days after it is applied; users can change this when applying".
- **Applied tags:** `TagBadge` shows a clock icon (`data-icon="inline-start"`) with an "Expires on …" tooltip, and expired tags are faded and struck through. The selector's selected list shows the relative expiry. The backend writes `expiry` with Python's `str(datetime)` (space separator, microseconds), so it is normalised to ISO 8601 before parsing.
- **Applying tags:** when a tag's config allows changing expiry, picking it in the `TagAssignmentSheet` selector opens an inline step (desktop dropdown and mobile drawer) to set the offset, prefilled with the config default. The set request then carries `expiry_offset`.
- **Playwright:** `tests/admin/tags/tagExpiry.spec.ts` covers the instance config (validation, details page, edit prefill) and a facility tag applied to a patient with a custom expiry.

Not in this PR: create forms (patient registration, encounter, appointment booking, delivery and request orders) apply the config's default expiry but don't offer a custom one yet. That needs their form state to carry a per-tag offset.

Against the `develop` backend, `expiry_metadata` is ignored without an error, so this should land with or after ohcnetwork/care#3792.

**Testing:** typecheck, lint and build pass. `tests/admin/tags/` (new spec plus the existing `tagconfig.spec.ts`) passes locally against `ENG-737-backup`.

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [x] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [x] Add or update Playwright tests for related changes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `32210a75af75`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.