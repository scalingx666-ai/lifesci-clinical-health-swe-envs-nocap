# Issue

**Title:** translate: the unit module says which units it means

## Description

`translate/units.py` and `mirobody/units` are two different things one letter
apart, and the first one's docstring had to open by saying so:

> Not `mirobody.units`, which is the UCUM engine in the library layer: it asks
> whether two arbitrary unit strings are interconvertible at all, **with no
> target**. This module imports its arithmetic from there.

`mirobody.units` is the UCUM algebra. `translate/units.py` answers a different
question — "give me this reading in the unit the catalogue declares for its
indicator", one target per indicator. Renamed to `canonical_units.py`.

**Why rename this one rather than move `mirobody.units` under `translate/`**
(the other way this was considered): `mirobody.units` is declared stable —
`mirobody/__init__.py`'s three imports, five import-linter contracts, and an
outside consumer — while `mirobody.translate.*` is documented as "internal and
moves without notice". Measured: `mirobody.units` has 8 importing files across
four packages (`indicator/`, `translate/`, `agent/tools/`, `server/routers/`),
so it is a primitive translate uses, not a part of translate.

`examples/02_standardize_a_reading.py` imported the deep path while a contract
named "translate has one front door" exists. It goes through
`mirobody.translate` now, which is what an example should teach.

No CHANGELOG entry: the front door exports the same three names
(`UNIT_CONVERSIONS`, `convert_to_standard`, `get_all_units_info`), so nothing
user-visible changed.

## Verified

8 reference points updated; a sweep for `translate.units` / `translate/units`
comes back empty. Suite unchanged against this branch's baseline — **5 failed /
1710 passed both before and after**, and all five are artefacts of running in a
worktree (three are agent-branch tests from PR #79 sitting in the local
`tests/`; two need `eval/testset.jsonl` and `CLAUDE.md`, both gitignored).
ruff, comment style, import-linter (6 contracts kept). The PHI baseline is
regenerated with `phi_lint.DEFAULT_TREES` and the diff is exactly the five path
renames, one for one.

This is item A of `internal/plans/1.4.x/2026-09-16-1.4.5-plan.md`. It is
independent of #79, so merge order does not matter.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0e2db3b1e7f7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.