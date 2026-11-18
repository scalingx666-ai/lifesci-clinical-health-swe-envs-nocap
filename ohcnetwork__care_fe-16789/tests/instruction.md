# Issue

**Title:** Add type check to CI

## Description

> [!NOTE]
> - 

Adds a `typecheck` script and runs it in the existing lint workflow on PRs to `develop`.

Nothing in CI was running `tsc`. The build transpiles via Rolldown without type checking, and `npm run build` is only invoked by the preview and Playwright workflows, so type errors could reach `develop` without failing a check. The one automated type check was `vite-plugin-checker` in the dev server, removed in #16788.

### Notes

Added to the existing `Lint Code Base` workflow rather than a new one, to reuse its `npm ci`. Runs before lint since it is faster, so failures surface sooner. CI only — not added to pre-commit hooks.

`npm run supported-browsers` runs first because `src/supportedBrowsers.ts` is generated and gitignored; without it `tsc` fails to resolve `@/supportedBrowsers`.

### Verification

Full workflow sequence run locally against current `develop`, all passing: `supported-browsers` → `typecheck` (0 errors, ~25s) → `lint` → `knip`.

Verified the generation step is required: without it, `tsc` fails with `TS2307: Cannot find module '@/supportedBrowsers'`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4c62defbbfac`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.