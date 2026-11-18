# Issue

**Title:** Remove vite-plugin-checker from the dev server

## Description

Removes `vite-plugin-checker`, which ran `tsc` and a type-aware ESLint program inside the dev server process and kept both resident for the whole session.

Dev server RSS, measured on this branch (same machine, same protocol — cold start, load `/` and `/src/index.tsx`, settle):

| | Dev server RSS |
| --- | --- |
| With `vite-plugin-checker` | 5486 MB |
| Without | 1686 MB |

Memory also grew over the life of a session rather than holding steady — a long-running dev server was observed climbing past 6.5 GB.

### Notes

Type and lint feedback is unchanged everywhere it is actually enforced: editor TS server, husky pre-commit hooks, and CI. The plugin was a fourth copy of checks already covered, and had `enableBuild: false`, so production builds are unaffected.

Run `npm run lint` or `npx tsc --noEmit` directly for a terminal check.

### Verification

- `npx tsc --noEmit` passes
- Dev server starts and serves `/` and `/src/index.tsx` (both 200), no checker output
- `vite-plugin-checker` fully removed from `package.json`, `package-lock.json` and `vite.config.mts`

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Chores**
  * Removed development-time TypeScript and ESLint checking from the Vite configuration.
  * Removed the associated development dependency.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1f0ec7651b12`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.