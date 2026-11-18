# Issue

**Title:** Use themeable icons in the facility sidebar

## Description

## Proposed Changes

- Replace the facility sidebar icons with inline SVG paths that inherit theme colors, with explicit active-state styling and stronger muted-layer opacity in dark mode.
- Adjust shared sidebar submenu styling: rows increase from 28px to 36px and lose right padding. This affects both facility and admin sidebars.
- Remove redundant sidebar SVG assets after converting them to inline paths.

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f09cd206775d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.