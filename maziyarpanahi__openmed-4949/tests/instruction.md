# Issue

**Title:** Write champion pointer and rollout state files atomically

## Description

## Problem

`ChampionPointer.save` (`openmed/eval/champion_challenger.py`), `RolloutStateMachine.save` and `save_audit` (`openmed/eval/rollout.py`) wrote their documents with `Path.write_text`. A crash or full disk mid-write leaves a truncated JSON file at the target path, which the next `load` rejects — the champion pointer / rollout state is then unrecoverable until the file is repaired by hand. .

## Root cause

`Path.write_text` truncates the destination in place before writing, so there is no moment at which the target holds either the old or the new content. Other state writers in the codebase already avoid this (`openmed/core/registry_slots.py::_write_state_atomic`, `openmed/service/jobs.py::_persist_locked`), but these three save sites predate that pattern and write pre-serialized strings.

## Fix

Add a text-level helper `_write_text_atomic(path, text)` in `openmed/eval/rollout.py`: write to a `NamedTemporaryFile` in the destination's own directory, `flush` + `os.fsync`, then `os.replace` onto the target; on any failure the temporary file is unlinked and the original stays byte-identical. All three save sites now go through it, so the saved content format is unchanged (same string, same encoding); `champion_challenger` imports the helper from its sibling module (no import cycle — `rollout` does not import `champion_challenger`).

## Testing

- New regression tests: `test_state_and_audit_saves_are_atomic_on_write_failure` (covers both `RolloutStateMachine.save` and `save_audit`) and `test_champion_pointer_save_is_atomic_on_write_failure`. Each saves successfully (asserting no temp files remain), then injects an `OSError` from `os.replace` and asserts the committed file is byte-identical and no temp files are left behind. Verified these tests fail against the unpatched code.
- `python -m pytest tests/unit/eval/test_champion_challenger.py tests/unit/eval/test_rollout.py -q` → 41 passed, 4 subtests passed.
- `ruff check` on the four touched files: clean.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b5bf9fc0c9c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.