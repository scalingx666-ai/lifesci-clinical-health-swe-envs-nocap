# Issue

**Title:** Use relative imports inside the library

## Description

.

## Bug
A few spots in the library still used package-level (absolute) imports, e.g. `from fhirclient.models.patient import Patient`. These break with `ModuleNotFoundError: No module named 'fhirclient'` as soon as the package is consumed under a different top-level name (vendored/renamed into another project) or in odd PYTHONPATH situations. This matches the maintainer preference on the issue to keep relative imports inside the library for portability.

## Root cause
Three remaining absolute imports:
- `fhirclient/client.py`: deferred `Patient` import in the `patient` property
- `fhirclient/_utils.py`: deferred `Bundle` import in `_execute_pagination_request`, plus the `TYPE_CHECKING` imports
- `fhirclient/models/fhirsearch.py`: `TYPE_CHECKING` imports

Reproduced on pristine main by copying the `fhirclient/` package to a temp dir under a different top-level name: the top-level import works (everything else is relative), but accessing `FHIRClient.patient` or calling `_utils._execute_pagination_request` raised `ModuleNotFoundError: No module named 'fhirclient'`.

## Fix
Converted all five to relative imports. Behavior-identical when the package is installed as `fhirclient`.

## Verification
- New regression test `tests/relative_imports_test.py` copies the package under a different top-level name and exercises both deferred imports (mocked, no network): fails on pristine main, passes with this fix.
- Full test suite: 491 passed (489 existing + 2 new) via `python -m pytest tests/`.
- `pip install .` from the branch and a plain import smoke test also pass.

CI status on this PR has not been observed; not claiming it is green.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2586be6fde3b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.