# Issue

**Title:** Open encounters full screen with appointment actions below the patient header (3.1)

## Description

## Proposed Changes

Encounter pages now take the full screen: no app sidebar and no workspace header. The actions that were portaled into the header move back into the encounter, below the patient card.

- **Appointment bar** attached below the patient card: Scan QR | Appointments board | Queue board | Token, with the start/finish prompt and Start Encounter / Complete / Mark for discharge on the right. Below `md` it collapses to Scan QR plus a ⋮ menu holding the rest.
- **Workspace switcher** moves next to Encounter Actions.
- **Back** is a small button above the patient card (`shift+←` via the existing `go-back` shortcut).
- The encounter section nav's sticky offset no longer reserves space for the header.
- `WorkspaceHeaderContent` / `WorkspaceHeaderSlot` / `WorkspaceHeaderContext` had no other callers and are removed (knip would flag them), along with their section in `docs/architecture.md`.

### Back behaviour

`goBack()` (`history.length > 1`) isn't a safe fallback here: a new tab or external link usually still has a previous history entry, so Back can leave CARE, and switching encounter sections pushes entries, so Back would step through sections instead of leaving the encounter.

`src/Utils/navigationTrail.ts` records in-app locations (push/replace aware) from `AppRouter`. The encounter's Back navigates to the latest recorded location outside `/encounter/:id/`, skipping section switches, historical-encounter views and encounter form pages. When there is none (new tab, reload, external link, deep link after login) it falls back to the patient page (`/facility/:facilityId/patient/:patientId`, or `/patient/:patientId` outside a facility).

### Testing

- `tsc`, eslint, prettier and knip are clean.
- `tests/facility/patient/encounter/encounterNavigation.spec.ts` updated for the new placement and labels, plus two Back steps: fallback to the patient page after switching sections, and returning to the appointments board the encounter was opened from. All 4 cases (desktop + mobile) pass locally against a production build.
- Manually checked at 1440, 900 and 390 px: no horizontal overflow, menu contents on mobile, and the sidebar/header return when leaving the encounter.

## Merge Checklist

- [x] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [x] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [x] Add or update Playwright tests for related changes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `37db2210c850`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.