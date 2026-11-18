# Issue

**Title:** fix: dispense dialog overflow and schedule sheet tint

## Description

## Proposed Changes

. Fixes two layout bugs that are live on `3.1/base`.

**Dispense "Change Location?" dialog**

- **Bug:** `Discard & Switch` sat 328px outside the dialog at 1440px wide, and the dialog showed two divider lines.
- **Cause:** #17008 added `shrink-0` to `Button` and borders to `DialogHeader` and `DialogFooter`. The two `w-full` buttons can no longer share the footer row, and a dialog with no body draws both borders.
- **Fix:** both buttons use `w-full sm:flex-1`, the same pattern as `CriticalActionConfirmationDialog`, and this footer drops its border.

**Create Schedule Template sheet**

- **Bug:** tall windows show a white band above the footer (119px at 1400px tall).
- **Cause:** #17016 moved the muted background from the sheet to the form area, which is only as tall as its content.
- **Fix:** add `flex-1` to the form area.

### Testing

Checked in a local build against the local backend:

- **Dialog:** the buttons stay inside it at 1440, 1024, 640 and 375px, stacking on phones, with one divider. `Stay here` and `Discard & Switch` both still work.
- **Sheet:** no white band at 1400px tall, and the last control still clears the footer at 1000px tall.
- **Static checks:** `tsc`, ESLint on the changed files, Prettier and `npm run build` pass.

No Playwright spec is added, and no existing spec covers either screen.

### Notes for review

- #17041 moves this dialog inside the new dispense drawer, which re-indents the same lines, and it doesn't include this fix. Whichever merges second needs to re-apply the three class changes.
- There's no Jira ticket yet, so `validate-jira-ticket` is expected to fail until the title has a key.

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0eebadfb4123`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.