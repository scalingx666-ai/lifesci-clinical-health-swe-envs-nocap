# Issue

**Title:** Disable source maps for production builds

## Description

<!-- entire-trail-link-start -->
https://entire.com/gh/ohcnetwork/-/trails/151/changes/care_fe/151
<!-- entire-trail-link-end -->

## Proposed Changes

- Production Vite builds no longer emit `.map` files or `sourceMappingURL` comments. `vite build` runs with mode `production`, so staging and production images stop publishing the maps next to the bundles.
- Non-production builds still generate source maps. Local `vite` dev is unchanged.

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

## Test plan

- [ ] `npm run build` completes and `build/assets` contains no `*.map` files
- [ ] Built JS bundles do not contain `sourceMappingURL`
- [ ] `npm run dev` still shows original sources in devtools

Made with [Cursor](https://cursor.com)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Chores**
  * Source maps are now generated for non-production builds and omitted from production builds.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `81e7515fdf4d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.