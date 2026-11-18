# Issue

**Title:** [ENG-887] Fix internal and external delivery batch failure and refine supply delivery limit UI

## Description

Entire-Checkpoint: 574e6f6865af
## Changes
* Mark as Complete is enabled only when all supply deliveries are either completed, abandoned or entered_in_error.
* Restricted users from adding more items than the upsert limit for dispatch and purchase deliveries by adding a callout for this scenario.
* Improved the Callout component by changing the badges type from string to ReactNode; updated the places that use the component
Fix: [ENG-887]

https://github.com/user-attachments/assets/20b99664-79b4-4b53-94ab-69639e7fec89


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


[ENG-887]: https://openhealthcarenetwork.atlassian.net/browse/ENG-887?atlOrigin=eyJpIjoiNWRkNTljNzYxNjVmNDY3MDlhMDU5Y2ZhYzA5YTRkZjUiLCJwIjoiZ2l0aHViLWNvbS1KU1cifQ

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Added a configurable limit for delivery datapoints per request, defaulting to 100.
  * Added loading indicators and disabled actions while deliveries are processing.
  * Improved order-loading labels to show item counts.

* **Bug Fixes**
  * Prevented adding or loading deliveries when the configured limit is reached.
  * Added clear alerts when delivery limits are exceeded.

* **Style**
  * Updated scheduling and warning callouts with clearer alert icons and presentation.

* **Documentation**
  * Documented the configuration option and its backend limit requirement.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1f0ec7651b12`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.