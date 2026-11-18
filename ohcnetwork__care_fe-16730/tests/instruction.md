# Issue

**Title:** [ENG-935] feat: integrate Shortcut for the new pharmacy (happy flow)

## Description

Fix:  ENG-935

This PR added shortcuts to new Pharm + integrate Shortcut across various dialogs and sheets
<img width="650" height="386" alt="image" src="https://github.com/user-attachments/assets/725ca037-0cef-4b9a-b367-8facf397fbe2" />

The happy enter flow

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [x] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [x] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

- **New Features**
  - Added keyboard shortcut indicators to medication, payment, dispensing, invoicing, and confirmation actions.
  - Added an **H** shortcut for placing eligible pharmacy items on hold.
  - Shortcut actions now target the appropriate visible, enabled control, including controls within open dialogs and overlays.
  - The keyboard shortcut command dialog can be opened through its registered shortcut.

- **Updates**
  - Standardized several action shortcuts for submitting, entering, and completing workflows.
  - Removed the billing payment-specific shortcut context and a hidden shortcut control.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1f0ec7651b12`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.