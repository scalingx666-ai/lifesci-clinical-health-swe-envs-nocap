# Issue

**Title:** Display patient blood group on patient profile

## Description

<!-- entire-trail-link-start -->
https://entire.io/gh/ohcnetwork/care_fe/trails/27
<!-- entire-trail-link-end -->

## Proposed Changes

The patient's blood group was stored and editable but never surfaced on the patient profile.

- Added a blood group entry to the general info section of the Demography tab (`src/components/Patient/PatientDetailsTab/Demography.tsx`), placed right after Sex.
- Reuses the existing `BLOOD_GROUP_LONG__*` i18n keys (same ones used by the encounter clinical history overview), falling back to `BLOOD_GROUP_LONG__unknown` when unset.

```tsx
{
  label: t("blood_group"),
  value: patientData.blood_group
    ? t(`BLOOD_GROUP_LONG__${patientData.blood_group}`)
    : t("BLOOD_GROUP_LONG__unknown"),
},
```

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

<!-- START COPILOT CODING AGENT SUFFIX -->

-

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9a6e36aeed97`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.