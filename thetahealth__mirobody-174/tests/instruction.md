# Issue

**Title:** bench: let word anchors bind their plurals

## Description

**What was wrong.** In `benchmarks/local_models/score.py` an English fact label bound only its exact word (`(?<![a-z0-9])lb(?![a-z0-9])`). So "about 153.7 lbs" or "153.66 pounds" never matched the `lb`/`pound` label, and a correct kilogram-to-pound answer failed. A local benchmark run on 2026-10-23 hit this on both phrasings of `h100-kilograms-to-pounds`.

**What changed.** A word label now also binds its plural (`s`/`es`), in both `_anchor_present` and `_anchor_spans`. Questions, expected facts and the case-manifest hash are unchanged, so saved results can be rescored with `score.py`.

**How to tell.**
- `tests/agent/test_local_eval_contract.py::test_unit_anchors_bind_plural_words_but_not_swapped_values` covers `lb`, `lbs` and `pounds`. A wrong value and swapped kg/lb values still fail.
- The new cases fail without the change; 54/54 pass with it.
- Rescoring 120 saved transcripts from that run with the new scorer changed exactly two results, both these conversions (fail → pass).

`ruff check` passes.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aef49c5ce81b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.