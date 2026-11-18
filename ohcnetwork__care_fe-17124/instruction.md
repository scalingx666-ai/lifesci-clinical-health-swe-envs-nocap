# Issue

**Title:** [ENG-1208] Show discharge disposition in Discharge Details

## Description

## Proposed Changes

Shows the discharge disposition in the encounter's **Discharge Details** card ([ENG-1208](https://openhealthcarenetwork.atlassian.net/browse/ENG-1208)). Until now the disposition picked in the discharge form wasn't shown anywhere.

- Adds one line under the discharge date, e.g. "Discharge Disposition: **Home**", in the card's existing text style. Nothing is shown when no disposition is set.
- Reuses the existing `discharge_disposition` and `encounter_discharge_disposition__*` strings, so there are no new translations.
- All 11 dispositions fit on one line in the 18rem panel, including the longest, "Other health care facility". A longer translation moves the value down to its own line.
- Extends the existing "Discharged status for an Inpatient encounter" shortcut test to check that the disposition picked in the discharge form ("Home") shows in the card.

**Not changed by this PR:** below the `xl` breakpoint (1280px), Discharge Details only appears in the summary panel's Actions tab, and that tab only shows while the encounter is still editable. So on phones and tablets, a completed encounter still shows no discharge date, advice or disposition.

### Testing

Ran on a local develop stack:

- Checked a completed encounter (disposition "Home") and a discharged one ("Other health care facility") at 1440px and 1280px, and on a 375px phone in the Actions tab.
- The updated test passes. It fails at the new check when the card change is reverted.
- `npx tsc --noEmit`, ESLint and Prettier pass.

Tagging: @ohcnetwork/care-fe-code-reviewers

<img width="301" height="305" alt="image" src="https://github.com/user-attachments/assets/8133b2b1-f44f-42dd-a3c8-862da131a56e" />

## Merge Checklist

- [x] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [x] Add or update Playwright tests for related changes

[ENG-1208]: https://openhealthcarenetwork.atlassian.net/browse/ENG-1208?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Discharge summaries now show the disposition, such as “Home,” when one is available. The disposition row is omitted when no disposition is set.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9640744c54c2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.