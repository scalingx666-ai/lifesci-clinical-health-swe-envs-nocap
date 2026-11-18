# Issue

**Title:** Add python_floor_inventory script for v6.0 floor review

## Description

## Summary

Adds `scripts/release/python_floor_inventory.py` that scans the repository for Python version guards, environment markers, workflow `python-version` entries, and documentation mentions that fall below a configurable floor (default 3.12). Outputs a human-readable table or machine-readable JSON containing only path, line number, and kind.

.

## Motivation

Raising the Python floor for the v6.0 native-core work is easier to review when the stale pieces are listed up front. The issue specifically requested an inventory covering the examples in `check_license_policy.py`, `pyproject.toml`, workflow files, and docs/README.

## Implementation

- New script following the style of other release scripts under `scripts/release/`.
- Regex-based scanners for `sys.version_info` guards, `python_version` markers, `requires-python`, workflow `python-version`, and numeric version mentions in Markdown.
- `--json` emits only path/line/kind (no file contents).
- Unit test under `tests/unit/release/` that builds a synthetic fixture tree and asserts the four required kinds appear.

## Testing

- `python3 -m pytest tests/unit/release/test_python_floor_inventory.py -q --noconftest` → 2 passed
- Ran the script against current master: it reports the expected findings (version_info_guard in check_license_policy.py:16, requires-python in pyproject.toml, multiple workflow python-version: "3.11", and docs mentions of 3.11 in getting-started.md and README*).

## Notes

The script is report-only and does not change any version settings. Findings are relative to the scanned root so the test can use a temporary tree.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b5bf9fc0c9c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.