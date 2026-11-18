# Issue

**Title:** release: cut 1.5.7

## Description

Cuts 1.5.7 from `main` @ `8bbffdf5` (#145–#152). One commit.

- `compose.yaml`, the source fallback, `server.json` and the Dockerfile name 1.5.7; `check_versions` passes.
- CHANGELOG's Unreleased becomes 1.5.7 (two stray blank lines removed).
- `AGENTS.md`, `CONTRIBUTING.md` and `docs/testing.md` still counted the 1.5.4 suite (332 tests, four modules). Re-measured in fresh venvs on a clone-shaped tree: `[test]` 409 passed / 161 skipped / 12 xfailed, `[test,app]` 620 / 99 / 12 (the 99 are the database cases without a DSN). `docs/testing.md` now lists all thirteen modules.

**Checked on this branch**
- ruff, compileall, lint-imports (6 kept), comment style, PHI baseline, bundle stamp, bare-interpreter library import: pass.
- pytest 620 passed / 99 skipped / 12 xfailed; the PostgreSQL gate against a throwaway `postgres:17`: 99 passed.
- `MIROBODY_VERSION=1.5.7 python -m build`: `check_wheel_data` 29/29, twine pass; the wheel in a fresh venv outside the checkout reports 1.5.7 and imports no third-party module.
- `docker build` (arm64, local): succeeds; in the image `__version__` is 1.5.7 and `/api/v1/health-indicators/confirm-code` is routed. Dockerfile, pyproject, MANIFEST and constraints are unchanged since 1.5.6, and no schema SQL changed.

**e2e before the tag** (`tests/e2e/harness.py`, all five stages; `scope.py` vs `f4fcee68` implicates all five because of #149 and #151): PASSED on an isolated server and worker running this branch (`/api/health` says 1.5.7), own database on PG 17, port 18190. 258 readings, no problems; the lipid answer cites its rows (`[r1]`–`[r3]`). Against the 10-13 run on #146 (265 readings, 141 LOINC-resolvable): 140 resolvable. The lab reports held or rose (56→56, 50→51, 24→24, demo 9→9). The gap is narrative imaging text: five chest-film findings not extracted, echo headings reworded, and the abdominal ultrasound photo named `肾脏` / `右侧肾脏无回声区` where it said `左肾` / `右肾` last time (2→0 resolvable). Nothing under `collect/`, `utils/llm` or `translate/` changed since that run, so this is the known extraction variance on narrative sections (open item E4), not a regression.

After merge: tag `1.5.7` → `pypi-release.yml` publishes PyPI, the GitHub Release and the Docker Hub image; I'll check the PyPI version endpoint and pull the image.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8bbffdf5a137`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.