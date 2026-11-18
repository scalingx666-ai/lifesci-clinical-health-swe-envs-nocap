# Issue

**Title:** Apply schedule departments and care team to encounters from appointments (3.1)

## Description

## Proposed Changes

Adds frontend support for schedule encounter defaults from ohcnetwork/care#3792 (backend branch `ENG-737-backup`, commit `ecd02f7f2`, which the Playwright CI job already runs against). A schedule can now carry default departments (`organizations`) and a default care team (`care_team`). When an encounter is started from one of its appointments, both are applied without anyone having to remember them.

- **Schedule create and edit sheets:** a new "Encounter defaults" section (`ScheduleEncounterDefaultsFields`) with the facility department selector and the existing care team field (`ReferralDefaultCareTeam`, reused with schedule wording).
  - The schedule list response omits the defaults, so the edit sheet fetches the schedule detail and loads it into the form with `values` / `keepDirtyValues`.
  - The edit sheet sends `organizations` and `care_team` only when they changed. The API rejects saved departments or members that have since left the facility, so resending unchanged defaults would block unrelated edits such as a rename.
- **Encounter from an appointment** (`AppointmentDetail` → `CreateEncounterForm`): the appointment's `token_slot.availability.schedule` defaults are passed in as `scheduleDefaults`.
  - The schedule's departments are preselected. They take precedence over the user's preferred departments and can still be changed.
  - The schedule's care team is listed in the sheet and assigned through `set_care_team_members` right after the encounter is created. If that call fails, the encounter is kept and a toast asks the user to add the care team from the encounter.
- **Types:** `ScheduleEncounterDefaults` (read, optional because list responses omit it) and `ScheduleEncounterDefaultsRequest` (write). Plus a `toCareTeamMembers` helper.

Against a backend without ohcnetwork/care#3792, the fields are absent from responses and ignored on writes, so nothing changes. This should land with or after ohcnetwork/care#3792.

Not in this PR: the schedule edit sheet's existing date handling shifts `valid_from`/`valid_to` back a day on save when the browser is not in the facility's timezone. That is unchanged here.

**Testing:** typecheck, lint and build pass. Manually verified against `ENG-737-backup`: created a schedule with two departments and a doctor + nurse care team, booked an appointment, and started a consultation. The sheet showed both departments and both members, and the created encounter had both departments and both care team members. Removing a care team member in the edit sheet saved correctly, and a name-only save sent no `organizations`/`care_team`. No Playwright spec yet.

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9331e85b08da`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.