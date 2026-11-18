# Issue

**Title:** fix: highlight default status tab in inventory To Dispatch / To Receive

## Description

On the inventory **To Dispatch** and **To Receive** pages, the status tabs showed no selected tab when the page first loaded, even though the list was already filtered by the default status. The tab only got highlighted after the user clicked it.

Before:
<img width="2412" height="1022" alt="image" src="https://github.com/user-attachments/assets/37092ccb-1534-4a99-966c-0ef90d28b3ec" />

After:
<img width="2560" height="929" alt="image" src="https://github.com/user-attachments/assets/35e06fd7-2b72-4a2a-9cc0-f86f1935410a" />

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [x] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ab8845ee88f2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.