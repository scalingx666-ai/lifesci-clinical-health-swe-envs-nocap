# Issue

**Title:** tests: cross-language identity ships with a clone

## Description

Ships `mirobody/tests/test_cross_language_identity.py`, so a terminology contributor can check from a clone that one analyte answers one code in every language. #88 could not run it, and it would have caught that PR's differential targets.

- **28 analytes agree** across en / zh / ja / ru / et (`SAME_ANALYTE`), pinning the series #88 merged.
- **13 do not yet** (`KNOWN_SPLITS`), each a strict xfail naming the fix: `urea` → urea nitrogen, English `direct bilirubin` → the conjugated code, vitamin D on two conventions, the Russian differential on `by Automated count` codes, and four names that answer nothing. A fix makes its row XPASS and fail until it moves up, so the list stays current. Checked by retargeting the two Russian neutrophil rows: exactly `[neutrophil count]` flipped.
- Two assertion messages in the existing local module referenced an undefined `code`; fixed.
- Docs that said "one module ships" (`docs/testing.md`, CONTRIBUTING, `mirobody/tests/__init__.py`, `conftest.py`, `pyproject.toml`) now describe two.

**Verified**
- Clean installs: `[test]` 17 pkgs, `[test,parse]` 74, `[test,app]` 146 all give **134 passed, 13 xfailed**.
- ruff, comment style, lint-imports (6 kept) clean.
- `python -m build` + `check_wheel_data.py` pass, and 0 test files in the wheel.
- Maintainers' local suite: no new failures against `main`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3e9173a1668e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.