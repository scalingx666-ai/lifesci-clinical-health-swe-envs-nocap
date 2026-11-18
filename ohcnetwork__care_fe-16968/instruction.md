# Issue

**Title:** fix: responsiveness issue in Product Knowledge page

## Description

<!-- entire-trail-link-start -->
https://entire.com/gh/ohcnetwork/-/trails/100/changes/care_fe/100
<!-- entire-trail-link-end -->

 

<img width="3868" height="1854" alt="image" src="https://github.com/user-attachments/assets/710a47c7-92b0-41cd-b46c-624ce5d379a2" />

<img width="378" height="849" alt="image" src="https://github.com/user-attachments/assets/b361599f-2392-4cc1-a140-2d2ded482f60" />


Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [x] Request peer reviews.
- [x] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Style**
  * Product names, identifiers, and codes wrap to remain visible in desktop tables and mobile cards.
  * Mobile product cards use a single-column layout, and action buttons retain their size.
  * The search area stays full-width, with a wider input on large screens.
  * Product headers stack on small screens and align horizontally on medium and larger screens.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `db0361fd84ae`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.