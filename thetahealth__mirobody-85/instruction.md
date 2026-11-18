# Issue

**Title:** scripts: doc-asset generators go local

## Description

`make_diagrams.py`, `make_demo_gifs.py` and `gen_zh_fold.py` produce
`docs/images/` and `mirobody/zh_fold.py`. None is a CI gate, and none is
needed to build, install or test a clone, so they move to `internal/`,
which is gitignored. `scripts/` keeps the five gates plus the crosswalk
report and the two e2e harnesses.

`mirobody/zh_fold.py`'s header named the generator; a clone has no such
file now, so it says what the table is made from instead.

Two defects in `gen_zh_fold.py` were fixed in the move, both pre-existing:
it wrote to `mirobody/indicator/zh_fold.py`, a path 1.5.0 deleted, so it
crashed; and its header template had drifted from the file it generates by
two em-dashes, which would have failed `check_comment_style` on the next
run. Verified by running it: the output is byte-identical to the tracked
file (3,336 mappings, 22,075 bytes).

## Verified

- `pytest -q` 1,987 passed, 4 skipped; `pytest -q mirobody` 69 passed
- `ruff`, `check_comment_style`, `lint-imports` (6 contracts), `stamp_bundle_version --check`
- `python -m build` + `check_wheel_data.py` on both artifacts
- `make_diagrams.py --check` from the new location: 8 diagrams match
- `test_doc_paths.py` caught one citation (`CHANGELOG.md` names the old
  path); allowlisted the way the deleted-in-1.5.0 scripts are

Known and left alone: the two frozen `archived/` READMEs link to
`../scripts/make_demo_gifs.py`, which now 404s. They describe 1.4.0.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0d532c83d0e7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.