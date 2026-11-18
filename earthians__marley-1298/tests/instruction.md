# Issue

**Title:** fix(allergy_seed): resolve ImportError for get_file_json during installation

## Description

## Summary
Fixes an installation crash where the setup script attempts to import `get_file_json` from the wrong namespace path.

### Cause
In the current version of the framework, `get_file_json` resides as a first-class function on the global `frappe` module context. Attempting to pull it from `frappe.utils` causes a terminal execution termination with an `ImportError`.

---

## Changes Made
- Changed `from frappe.utils import get_file_json` to `from frappe import get_file_json` inside `allergy_seed.py`.

---

## Verification
1. Run app installation again:
   ```bash
   bench --site develop.localhost install-app healthcare
   ```
2. **Expected Result:** DocTypes update successfully past 100% with no import exceptions thrown.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3891d60586b6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.