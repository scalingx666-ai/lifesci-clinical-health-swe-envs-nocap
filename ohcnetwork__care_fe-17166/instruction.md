# Issue

**Title:** Hide location Inventory and Pharmacy when Inventory Usage is unset

## Description

## Proposed Changes

- Hide Inventory and Pharmacy in the location sidebar when Inventory Usage is None or unset.
- Add a Playwright regression that verifies both groups are visible for a Consumption location and disappear after its usage is reset to None.

. External Supply remains exclusive to Store locations.

## Verification

- ESLint, Prettier, and TypeScript checks passed.
- The Playwright regression passed in Chromium against a seeded local backend.
- A Chromium check of the location sidebar covered missing usage and all five Inventory Usage values. It also verified that Purchase Orders appear only for Store.

The PR title check requires a Jira key. This follow-up has no Jira key assigned in the request.

## Merge Checklist

- [x] Add specs that demonstrate the bug or test the new feature.
- [x] Add or update Playwright tests for related changes

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Pharmacy and Inventory navigation links are now shown only when inventory usage is enabled. Locations with no inventory usage retain access to the location page without those links.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `31f590ff3446`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.