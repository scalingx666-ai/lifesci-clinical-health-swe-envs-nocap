# Issue

**Title:** Handle missing Python tests in CI

## Description

The `build (3.11)` GitHub Actions job was failing in `make test`, not in dependency installation or static analysis. The test target invoked `unittest` with a literal `tests/test_*` module path, which breaks when the repository has no matching Python test files.

- **Root cause**
  - `make test` ran:
    ```make
    uv run -m unittest tests/test_*
    ```
  - With no `tests/test_*.py` files present, `unittest` attempted to import `tests/test_*` as a module and failed with `ModuleNotFoundError`.

- **Change**
  - Updated the `Makefile` test target to detect whether any `tests/test_*.py` files exist before invoking Python tests.
  - When tests are present, it now uses `unittest discover`.
  - When no matching files exist, it exits cleanly with an explicit skip message.

- **Behavior**
  - Test execution remains unchanged for repositories that add `tests/test_*.py` files later.
  - Repositories without Python tests no longer fail CI on the test step.

```make
@if [ -d tests ] && find tests -maxdepth 1 -type f -name 'test_*.py' -print -quit | grep -q .; then \
	${PYTHON} -m unittest discover -s tests -p 'test_*.py'; \
else \
	echo "No test files found in tests/; skipping test execution."; \
fi
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f2bd3cfc3cef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.