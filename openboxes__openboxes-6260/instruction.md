# Issue

**Title:** OBLS-1003 Tighten four frontend regression tests

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:**
https://openboxes.atlassian.net/browse/OBLS-1003 ()

**Description:**

Addresses the four review comments on #6253. Test-only; no application code changes.

- **`cycle-count/cycleCountSteps.test.jsx`**: `getCurrentLocation` caches locations by id for the
  life of the module, so the first test's bin-enabled `loc1` was reused by every later test in the
  file. The bin location now has its own id (as `cycleCountReporting.test.jsx` already does), and a
  later test checks that the default location shows no bin column.
- **`hooks/options-data/useOptionsFetch.test.js`**: the locale step also passed a new location
  object, so the test still passed with locale refetching removed. It now reuses the location
  object and checks the call count after each step.
- **`hooks/useConnectionListener.test.js`**: after unmount, an `online` event must not start a
  reconnection, and a new test checks that an `offline` event does nothing.
- **`hooks/useWindowWidthCheck.test.js`**: checks that the `resize` callback that was added is the
  one removed on unmount (the hook's last value stays the same after unmount either way).

## Verification (local, Node 14)

- Each fix was checked against the defect it targets: with the hook changed to ignore locale
  changes, drop its listeners, or share the cached location, the old test passed and the new test
  fails.
- `npm test`: 238 suites passed, 6 skipped; 2329 tests passed, 76 skipped, 0 failed.
- ESLint clean on the four files.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bc00ffee29f6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.