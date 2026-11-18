# Issue

**Title:** Fix CodeQL findings in diagnostics, storage and CI permissions

## Description

## What this changes

The first CodeQL scan flagged diagnostics, storage paths, credential hashing and workflow permissions. This PR removes response messages and credential fragments from diagnostics, prevents vendor exception text from leaking through storage logs, keys log fingerprints, bounds resolved local paths, matches the exact Mandrill SMTP host, and limits the test workflow token to repository reads.

Provider identities previously used only eight MD5 hex characters for an internal email. Invented Garmin ids `102` and `44553` produced the same address, and `create_user` reuses an existing email. New synthetic addresses use 128 bits of SHA-256; existing provider bindings are looked up first and are not migrated. Extraction failures now return a fixed public message.

The log correlation handle now uses a process-local key, so fingerprints change after a restart and cannot be compared with an offline dictionary of candidate file keys or short credentials.

## Which gate you ran

- [x] `pytest -q` against this worktree's source, both public test roots plus the new synthetic regressions: **782 passed, 107 skipped, 12 xfailed**. This worktree does not contain the maintainers' ignored regression suite. The database module was also run against disposable PostgreSQL 17: **107 passed**.
- [x] New `tests/server/test_codeql_security.py`: **27 passed**. Covers response/log separation, full masking, keyed fingerprints, exact SMTP selection, the old synthetic-id collision, storage traversal/symlink refusal, unchanged ephemeral index bytes, vendor-error redaction and extraction error responses.
- [x] `ruff check mirobody examples tests/server/test_codeql_security.py`
- [x] `python -m compileall -q mirobody`
- [x] `lint-imports`: **6 kept, 0 broken**; verified `mirobody.__file__` resolves inside this worktree.
- [x] Bare `python3 -c 'import mirobody.kernel.meds, mirobody.kernel.query'`
- [x] PHI lint: **0 problems**; comment-style check and `git diff --check` pass.
- [x] Genomics benchmark unit checks: **37 tests, 2 skipped**; health-record benchmark unit checks: **3 tests passed**.

The tests are synthetic public evidence and are intentionally added under the normally ignored `tests/server/` directory; minimal installs skip that directory at collection time.

## CodeQL verification

All 50 initial alerts have a documented disposition:

| Alerts | Disposition and evidence |
| --- | --- |
| #1–#4 | Explicit least-privilege workflow permissions. |
| #5–#8 | Resolved-path containment with a directory separator boundary; traversal, sibling-prefix and symlink regressions pass. The previous check already rejected escape paths. |
| #9 | Fixed public extraction failure message; arbitrary exception content is not returned. |
| #16, #26–#27 | Full credential masking and event/status-only response logs. |
| #49 | Longer synthetic provider identity; the old MD5-prefix collision is reproduced by two invented ids. Existing links retain their account. |
| #50 | Exact Mandrill SMTP hostname, including case/trailing-dot normalization; lookalike domains select ordinary SMTP. |
| #10–#15, #17–#25, #28–#44 (32 alerts) | Verified false positives: the sink receives a fingerprint, not the original credential/file key. The helper is further hardened to a random-key HMAC. The separate storage vendor-exception traceback leak is fixed in code. |
| #45–#46 | Verified false positives: model/configuration metadata and API-key **variable names**, not values. A synthetic key-value regression verifies this. |
| #47 | Verified SARIF flow from Garmin OAuth1 request tokens into the encrypted ephemeral-state **lookup index**, not a human password verifier. The index remains byte-identical; values are Fernet-encrypted. |
| #48 | Verified SARIF flow from **encrypted password ciphertext** into a diagnostic fingerprint after failed decryption, not password storage/verification. |

The PR scan produced two additional findings (#51–#52), both verified false positives on the keyed diagnostic fingerprint. CodeQL propagates secret labels through the digest. Regression tests verify that raw keys/ciphertext and vendor exception text are absent from logs, and that a different HMAC key produces a different handle. These and the 36 baseline false positives were individually marked `false positive`, with reasoning recorded on each GitHub alert. No query rules were disabled or excluded.

CodeQL passed after triage, with **0 open alerts for the PR head**. Main still has the 14 code-addressed alerts until this PR is merged and main is rescanned. Final commit `2b7099c7c73a352fd4e3902f50a756078c862c25` passes all 10 GitHub checks, including Python/Actions analysis, the CodeQL alert gate, Python 3.12/3.13 builds and Linux/macOS/Windows installation checks.

## Which benchmark it moves

None. No resolver, catalogue, bundle, observation writer or database schema changes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `002508a0bee2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.