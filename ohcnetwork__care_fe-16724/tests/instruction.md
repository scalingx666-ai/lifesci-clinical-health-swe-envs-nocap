# Issue

**Title:** [ENG-938] 🐛 Fixes conditional hook call in useCurrentFacility

## Description

ENG-938

## Problem

`useCurrentFacility` broke the Rules of Hooks.

The helper `extractFacilityId` threw an error when the path was not a facility route. The throw stopped `useQuery` from running. React counts hook calls in order on every render. If a component rendered one time inside a facility route, and one time outside it, the hook count changed. React can then attach state to the wrong hook. This corrupts state or stops the render.

`useCurrentFacilitySilently` made the problem visible. It called the hook inside a `try` block and caught the error.

## Fix

- `extractFacilityId` returns `undefined` when the path is not a facility route. It does not throw.
- `useCurrentFacilitySilently` holds the data fetch. It always calls `useQuery`. The new `enabled: !!facilityId` option stops the fetch when there is no facility id. The `queryKey`, the `staleTime` and the `query(facilityApi.get, ...)` call keep the same shape.
- The default export `useCurrentFacility` calls `useCurrentFacilitySilently()` first, at the top level. It throws only after all hooks run. The order of the hooks is now the same on every render.
- `useCurrentFacilitySilently` no longer uses `try`/`catch`.

## Compatibility

The public return types stay compatible:

- `useCurrentFacility()` still returns `facilityId` as a `string`. The `if (!facilityId) throw` check narrows the type. No call site of the default export needs a change.
- `useCurrentFacilitySilently()` returns `facilityId: string | undefined` and `facility` as before. It now also returns `isFacilityLoading`. No call site reads that field today, so this is an addition only.

There is no behaviour change. Inside a facility route, the query runs as before. Outside a facility route, the query does not run.

## React Doctor: before and after

Rule `react-doctor/rules-of-hooks`:

| Report | Occurrences |
| --- | --- |
| Before | 1 |
| After | 0 |

Before (`npx react-doctor@latest --verbose`):

```
✖ Hook called conditionally
  react-doctor/rules-of-hooks
  src/pages/Facility/utils/useCurrentFacility.tsx:39
```

```
Bugs: 17 errors, 510 warnings
Share: https://react.doctor/share?p=care_fe&s=43&e=21&w=1313&f=404
```

After (`npx react-doctor@latest --verbose`):

```
(no react-doctor/rules-of-hooks occurrence)
```

```
Bugs: 16 errors, 510 warnings
Share: https://react.doctor/share?p=care_fe&s=44&e=20&w=1313&f=403
```

Total errors go down from 21 to 20. The change adds no new React Doctor finding.

## Checks

- `tsc --noEmit`: no new error. One error stays: `src/components/ErrorPages/BrowserWarning.tsx(7,31): Cannot find module '@/supportedBrowsers'`. The build generates that module. `knip.json` already lists it as unresolved. The error also exists before this change.
- `eslint src/pages/Facility/utils/useCurrentFacility.tsx`: clean.
- `prettier --write` applied to the changed file.
- Playwright E2E tests: not run. This environment has no local backend.

## Files changed

- `src/pages/Facility/utils/useCurrentFacility.tsx`

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

## Summary

* **Bug Fixes**
  * Non-facility pages no longer trigger errors when facility information is checked.
  * Facility data is requested only when a facility is identified in the route, avoiding unnecessary requests.
  * Silent facility checks now provide consistent facility details and loading status when available.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8b5066744940`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.