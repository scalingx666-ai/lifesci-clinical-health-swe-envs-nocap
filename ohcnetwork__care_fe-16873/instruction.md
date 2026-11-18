# Issue

**Title:** [ENG-436] fix: sub_queue handling and mobile UI polish for queue board redesign

## Description

<!-- entire-trail-link-start -->
https://entire.io/gh/ohcnetwork/care_fe/trails/50
<!-- entire-trail-link-end -->

Stacked on #16871.

## Proposed Changes
- Fix \`sub_queue\` handling in token actions and service-point UI components
- Enhance mobile UI with the service point selector and improve layout for the Waiting and Recall sections

fixes: ENG-436

figma https://www.figma.com/design/Z93EYKSa1MdBmXndsMBJSQ/Care---Master?node-id=39564-32857&t=yrxyVq32Krk8XNn3-0

<img width="859" height="567" alt="image" src="https://github.com/user-attachments/assets/6370e656-94b4-4207-a58e-3b04e45fdb26" />

<img width="399" height="789" alt="image" src="https://github.com/user-attachments/assets/ded0525d-ce78-45d5-a5eb-1976c4a40d72" />



Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [x] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes


> This PR is stacked on top of #16871 and only diffs the additional commits. It should be rebased/retargeted to \`develop\` once #16871 merges.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a4526c121739`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.