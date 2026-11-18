# Issue

**Title:** [ENG-1000] Pixel-art SVG Heartbeat animation for loading animation

## Description

> [!NOTE]
> JIRA Ticket: ENG-1000

## Proposed Changes

- Adds [Care UI's Loading Animation SVG](https://careui.ohc.network/#loading-animation-svg)
- Also show a static pixel-art heart while loading the entrypoint bundle.

https://github.com/user-attachments/assets/9f200c62-7c40-4ac4-9035-d25cf87999c3

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [x] Add specs that demonstrate the bug or test the new feature.
- [x] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files.
- [x] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [x] Request peer reviews.
- [x] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added a pixel-art loading animation that transitions between a heart and Care UI logo.
  * Added localized “loading” text with animated dots.
  * Improved loading visuals with heartbeat and breathing effects.

* **Accessibility**
  * Added an accessible label describing the loading animation.

* **Style**
  * Updated loading animation styling and removed obsolete logo animation styles.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1f0ec7651b12`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.