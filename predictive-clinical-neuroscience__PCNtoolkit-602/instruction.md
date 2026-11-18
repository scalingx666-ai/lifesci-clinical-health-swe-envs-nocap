# Issue

**Title:** fix: warn once per version on model migration

## Description

## Problem

Loading a model saved with an older PCNtoolkit version prints the same migration warning many times. Because the timestamp in the message changes second to second, repeats are never treated as duplicates.

## Cause

Two things add up:

1. `MigrationRegistry.migrate()` called `Output.warning()` once per migration function, per component and per response variable, so the count scales with the size of the model.
2. `Output.warning()` prefixes every message with a timestamp and pid, so no two emissions ever have identical text, and Python's warning dedup never sees a repeat.

## Fix

Track the `(saved version, current version)` pairs the registry has already warned about, and emit the warning only the first time a pair is seen. The migrations themselves still run on every call; only the warning is deduplicated.

## Why a set rather than dropping the prefix

The issue suggests removing the timestamp/pid prefix so that Python's own dedup applies. That works under default filters, but any caller that installs `simplefilter("always")` (pytest does) bypasses the registry check and would still see every repeat. Keying on the version pair makes the behaviour independent of whatever warning filters the caller has installed, while the timestamp is kept so log lines can still be correlated.

This matches the issue's expectation of one warning per saved version. The response-variable counts in the issue's example message would need aggregation at `NormativeModel.load()` level, since `migrate()` only ever sees one dict at a time. Happy to do that as a follow-up if it is wanted.

## Tests

Four regression tests added to `test/test_util/test_migration.py`, following that file's existing style (fresh registry per test, `patch` on `Output.warning` plus `call_count`):

- `test_009` — five calls for the same saved version warn once (previously 10)
- `test_010` — two distinct saved versions warn once each
- `test_011` — deduplication does not skip the migration itself
- `test_012` — a fresh registry warns again, so no state leaks

All four fail on unmodified `dev` and pass with the fix.

Related tests run locally:

- `test/test_util/` — 38 passed
- `test/test_norm/test_normative_model_helper.py` — 14 passed
- `test/test_core/test_pretrained_model.py` — 7 passed
- `test/test_math/test_basis_functions.py` — 25 passed, 1 failure described below

`ruff check` and `ruff format --check` are clean on both changed files.

Note: `test_composite_from_dict_passes_version_to_parts` also fails on unmodified `dev` in my local environment. It is an environment artifact: the installed package metadata reports 1.3.0 while `pyproject.toml` says 1.4.0, and three migrations are registered with `introduced_in="1.4.0"`, which is why that test sees exactly three warnings where it expects none. CI installs with `pip install -e ".[dev]"`, so metadata matches the source tree there.

## AI usage

AI was used to generate this code, using an OpenCode coding agent. Stated here per this repository's contribution guidelines requiring AI use to be declared in every pull request.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f83435cf6e08`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.