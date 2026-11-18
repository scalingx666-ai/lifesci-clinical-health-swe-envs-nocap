# Issue

**Title:** OBLS-1003 Build the frontend bundle in the frontend test job

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:**
https://openboxes.atlassian.net/browse/OBLS-1003 (follow-up: faster CI for the existing backend tests)

**Description:**

## What

The "Test Pull Request" backend job takes about 11 minutes, and about 4 of them go to building the webpack bundle:
`processResources` depends on `npm_run_bundle`, so `./gradlew jacocoTestReport` builds the frontend before any test
runs. The backend tests do not need it.

- `backend-tests.yml`: `jacocoTestReport -x npm_run_bundle`.
- `frontend-tests.yml`: `npm run bundle` as a step of the existing frontend job, after `npm test` (it runs even
  when a test fails, so both kinds of failure show in one run). The production build and ESLint (webpack's
  `ESLintPlugin`) are still checked on every pull request and push, under the same check name as the jest tests,
  now in parallel with the backend tests instead of before them.

Expected: the backend job drops from about 11 to about 7 minutes. The frontend job grows from about 1-2 to about
6 minutes and runs at the same time, so a pull request waits about 7 minutes instead of 11.

**Also applies to `develop`.** The two workflow files are identical on `develop`, so this commit cherry-picks
cleanly there.

## Verification (local)

`jacocoTestReport -x npm_run_bundle` in fresh clones with no webpack output, `TZ=UTC TEST_DATABASE=mysql:8.0.36`:

| Base | test | integrationTest |
|---|---|---|
| `feature/obaf-integration` a2d379b64 | 1,157 passed, 11 skipped (same as with the bundle) | 68 passed, 2 skipped (same) |
| `develop` 94f393a24 | 1,604 passed, 11 skipped | 75 passed, 2 skipped |

`npm ci && npm run bundle` on Node 14.21.3 / npm 6.14.18: exits 0. With an ESLint error added to a `.jsx` file it
exits 1 and reports the error, so the frontend job fails a pull request that breaks the lint, as the backend job did before.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bc00ffee29f6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.