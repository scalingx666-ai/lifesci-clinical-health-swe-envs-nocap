# Issue

**Title:** [ENG-753] Resolve react-hooks/preserve-manual-memoization violations

## Description

> [!NOTE]
> JIRA Ticket: ENG-753

## Proposed Changes

When we upgraded `eslint-plugin-react-hooks` to v7, its `recommended` config started shipping the React Compiler rules. To avoid blocking that (already large) PR, these rules were downgraded to `warn` and slated to be addressed incrementally. This PR fully resolves one of them: `react-hooks/preserve-manual-memoization`.

React Compiler is **not** enabled in the build, so the existing `useMemo`s do real runtime work. Every fix preserves behavior. There were two distinct causes:

- **Optional-chaining dependency mismatch** (4 files): dependency arrays used `x?.results` while the memo body accessed `x.results`, so the compiler inferred a different/broader dependency than declared. Hoisted the accessed value into a local const so the manual deps match exactly what the compiler infers, keeping memoization intact.
  - `LocationMultiSelect.tsx` (`searchLocations`)
  - `AdministrationTab.tsx` (`administrationResults`)
  - `app-sidebar.tsx` (`userOrganizations`)
  - `BedChargeItemsTable.tsx` (`chargeItemResults`)
- **Compiler declines to memoize a primitive** (2 files): `isDisabled` is a boolean derived from cheap `.some()` calls with no downstream identity benefit, so the compiler correctly drops the memoization. Replaced `useMemo` with a plain expression (identical value each render).
  - `RoleOrgSelector.tsx` (also dropped the now-unused `useMemo` import)
  - `FacilityOrganizationSelector.tsx`
- Removed the `"react-hooks/preserve-manual-memoization": "warn"` override in `eslint.config.mjs` so the recommended `error` level now applies and prevents regressions.

Verified: full-project ESLint reports **0** `preserve-manual-memoization` messages at `error` severity, and `tsc --noEmit` shows no new type errors in the edited files. The remaining React Compiler rules (`set-state-in-effect`, `refs`, etc.) stay at `warn` and are out of scope here.

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

N/A - lint-only refactor with no behavioral or UI changes.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Refactor**
  * Simplified organization and role selector disabled-state calculations without changing behavior.
  * Streamlined data processing for locations, medication administrations, sidebar organization selection, and billing charge items.
* **Chores**
  * Updated linting configuration to remove an outdated React hooks warning while retaining other hook checks.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8160376515fd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.