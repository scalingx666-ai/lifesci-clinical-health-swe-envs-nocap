# Issue

**Title:** chore(frontend): update dependencies

## Description

## What does this change?

Raises every frontend dependency to its latest release within the majors the app can take without a migration, and refreshes `bun.lock`.

| Package | From | To |
| --- | --- | --- |
| `vitest` | 4.1.11 | 5.1.0 |
| `@vitest/browser-playwright` | 4.1.11 | 5.1.0 |
| `vitest-browser-svelte` | 2.2.1 | 3.1.0 |
| `@playwright/test`, `playwright` | 1.64.1 | 1.65.1 |
| `@sveltejs/kit` | 2.70.3 | 2.70.4 |
| `@sveltejs/adapter-node` | 5.5.7 | 5.5.8 |
| `vite` | 8.3.5 | 8.3.8 |
| `@lucide/svelte` | 1.63.0 | 1.73.0 |

The rest are minor/patch bumps (eslint, eslint-plugin-svelte, typescript-eslint, prettier, tailwindcss, `@tailwindcss/vite`, globals).

`vitest-browser-svelte` 3 makes `render()` async, so the four browser specs now `await` it. No app code changes.

Held back:

- `@sveltejs/kit` 3 and `@sveltejs/adapter-node` 6 (needs Kit 3). Kit 3 removes `kit.env.publicPrefix` in favour of a declared `src/env.ts` (`$app/env/*`), which is how `VITE_API_URL` reaches the browser today. Trying it gave 58 svelte-check errors in 36 files (typed `resolve()` paths, read-only `page.url`, `goto` without `noScroll`). That needs its own PR.
- `typescript` 7: `typescript-eslint` 8.72.2, the latest, refuses to run on TS 7.

## Why?

Keep the frontend toolchain current. The two open Dependabot alerts for `frontend/` (#99, #100, both low, `@sveltejs/kit`) are fixed only in Kit 3.0.0, so they stay open until the Kit 3 migration.

## How did you test this?

In `frontend/`:

- `bun install --frozen-lockfile`: passes
- `bun run check`: 0 errors, 1 warning (same as on `main`)
- `bun run lint`: passes
- `bun run format:check`: passes
- `bun run test:unit --run`: 32 files, 387 tests passed
- `bun run build`: passes
- `bun run test:e2e`: 260 passed, against the bundled mock API (run on another port because 8787 was busy locally)
- `pre-commit run --all-files` from the repo root: all hooks pass

Not tested: the Docker image and a run against a real backend.

## Breaking change

None.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Chores**
  * Updated development tooling to keep the project’s build and quality checks current. No user-facing feature changes are included in this update.
* **Tests**
  * Browser checks now wait for components to render before verifying charts, navigation links, providers, and connections. Existing checks remain unchanged, with more consistent timing during automated validation.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7ca121dd4e48`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.