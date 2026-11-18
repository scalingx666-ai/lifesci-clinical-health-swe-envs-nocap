# Issue

**Title:** [ENG-748] fix: text overflow in Administration Table

## Description

Enhance text wrapping and prevent overflow issues in Mobile View. The main change is the addition of the `text-wrap` class to various elements to ensure long text displays correctly.

Before:
<img width="410" height="827" alt="image" src="https://github.com/user-attachments/assets/4c05f5ab-38e0-4aca-807b-8b0fc59d1c54" />

After:
<img width="408" height="741" alt="image" src="https://github.com/user-attachments/assets/3191f339-938c-4221-9649-b01f38830d87" />

Tagging: @ohcnetwork/care-fe-code-reviewers
[ENG-748]

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [x] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [x] Request peer reviews.
- [x] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes


[ENG-748]: https://openhealthcarenetwork.atlassian.net/browse/ENG-748?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Style**
  * Improved text wrapping for medication dosage instructions and administration timestamps so long content breaks cleanly.
  * Enhanced readability of grouped and individual medication details across varying screen sizes.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dd3299d27f4a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.