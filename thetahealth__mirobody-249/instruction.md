# Issue

**Title:** fix(import): find the Apple Health export by its HealthData root

## Description

## What this changes

. `open_export` now tries `export.xml` first, then picks the `.xml` in the export folder (skipping `*_cda.xml`) whose root element is `HealthData`. This works for both a zip and an unpacked directory, so an iPhone set to Chinese (`apple_health_export/导出.xml`) imports. `import --into` now reports a missing export as one `mirobody import: ...` line, matching the dry-run path, instead of a traceback.

## Which gate you ran

Ran on GitHub Actions (`test-build.yml`) on my fork, Python 3.12 and 3.13:

- [x] `pytest -q` (full local suite, both roots): 1318 passed, 124 skipped, 12 xfailed
- [x] `pytest -q mirobody` (minimal install): 793 passed, 195 skipped, 12 xfailed
- [x] `lint-imports`: 6 kept, 0 broken
- [x] `uvx ruff check mirobody examples` (lint gate)
- [ ] `python -m benchmarks.run_eval`: not applicable, no resolver or bundle change

The new `mirobody/tests/test_apple_export_lookup.py` covers zip and directory exports named `export.xml` and `导出.xml`, plus a zip or directory with no `HealthData` document. The `导出.xml` cases and both refusal cases fail on `main`.

## Which benchmark it moves

None.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9d292f8ba61a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.