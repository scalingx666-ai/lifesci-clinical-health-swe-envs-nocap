# Issue

**Title:** [ENG-1209] Add encounter class filter to the account list

## Description

## Proposed Changes

Adds an **Encounter Class** filter to the account list (Billing → Accounts, and the patient's Accounts tab).

- Picking a class shows only accounts whose primary encounter has that class. Accounts with no primary encounter drop out whenever a class is picked.
- Reuses the existing `encounterClassFilter`, so the options are the facility's configured encounter classes, and the choice is kept in the URL like the other account filters.
- Sends `encounter_class` to the account list API.

**Depends on ohcnetwork/care#3829** (ENG-1209), which adds `encounter_class` to `AccountFilters`. Without it the backend ignores the parameter and the list stays unfiltered.

### Testing

Ran against ohcnetwork/care#3829 (`ENG-1209`) on a fresh database built from its migrations and `load_fixtures`, with 3 extra active accounts that have no primary encounter. Facility "FACILITY WITH PATIENTS", status Active:

| Encounter Class | Accounts shown |
| --- | --- |
| (none) | 5 |
| Ambulatory | 1 (the account linked to an ambulatory encounter) |
| Virtual | 1 (the account linked to a virtual encounter) |
| Inpatient | 0 |

- The request carries `encounter_class=<code>`; clearing the chip drops it.
- Reloading a filtered URL keeps the chip and the filtered list.
- `npx tsc --noEmit` and ESLint pass.

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

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Added an encounter-class filter to the account list. Its selection is reflected in account results.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1b35871c605a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.