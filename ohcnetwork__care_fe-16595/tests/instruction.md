# Issue

**Title:** Fixes Appointment slots query cache key omits resource type/id

## Description

## Proposed Changes

 

Include `resourceType `and the resolved resource ID in the appointment slots query key.
Reuse the same resolved resource ID in both the query key and request body.
Prevent cached availability from one resource being temporarily displayed for another resource at the same facility and date.
No behavior changes beyond correctly scoping the TanStack Query cache.

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

* [ ] Add specs that demonstrate the bug or test the new feature.
* [ ] Update [product documentation](https://docs.ohc.network/).
* [x] Ensure that UI text is placed in I18n files.
* [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
* [x] Request peer reviews.
* [ ] Complete QA on mobile devices.
* [ ] Complete QA on desktop devices.
* [ ] Add or update Playwright tests for related changes.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

## Summary

* **Bug Fixes**
  * Improved appointment day-slot loading by deriving a single, consistent resource identifier used for both the day-slots request and the related cached results.
  * Updated availability caching to account for resource type and the selected date range, reducing stale or mismatched slot displays when filters change.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bcb288a17ba2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.