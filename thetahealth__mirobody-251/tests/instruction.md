# Issue

**Title:** observations: a name that folds to nothing is no name

## Description

Part of #235 (symptom C, the nameless row).

### What was wrong

`observations.prepare` refused a reading whose name was empty after trimming whitespace. Two kinds of name passed that check and still produced a row with no visible name:

- **Punctuation only.** `：` NFKC-folds to `:`, and `name_key` strips trailing punctuation, so the series key ends up as `""` and the reading is stored under a blank local series.
- **Invisible characters only.** A zero-width space (U+200B), a byte-order mark or a soft hyphen survives the fold and prints as nothing. Text extracted from a PDF can carry these, and nothing upstream strips them.

As the reply on #235 says, either is one way to get the nameless uric acid row reported there. This PR closes both paths; whether one of them is the path the reporter hit depends on that row's `name_text`, which is still asked for in the issue.

### Change

- The gate requires a character that shows in `standardize.name_key(name)`, the key every series is built from. Such a reading is rejected as `no-name`, the reason an empty name already gets. The key itself is unchanged, so no stored series splits.
- A row stored before this gate is refused when amended. `redate()` amends a report row by row; it now leaves such a row on its old date instead of failing half way (on `main` the endpoint answered 500 on every retry). The row is counted neither `moved` nor `skipped`, because the Data page and the agent word `skipped` as "already had a reading that day". Any other refusal, such as a future date, still fails the move.

### Test

- `mirobody/tests/test_extraction_regressions.py::test_a_name_that_folds_to_nothing_visible_is_no_name` covers `""`, `"  "`, `"："`, `":"`, `"。"`, `" ， "`, `"​"`, `"﻿"`, `"­"` and `"​："`. On `main`, every case except the two whitespace ones fails.
- `mirobody/tests/test_postgres_regressions.py::test_a_report_with_a_row_stored_without_a_name_can_still_be_redated` stores a `：` row the way the old write path did, then re-dates its report: a future date is still refused, and a past date moves the other two rows and returns `(2, 0)`.

On this branch merged with current `main`:

```
pytest -q, [app,test] + PostgreSQL 17   → 1600 passed, 12 xfailed
lint-imports → 6 kept · ruff → clean · compileall → ok · bare library import → ok
comment style → 0 · versions → 1.5.10 · PHI lint → clean
```

The rest of #235 is not addressed here:

- **Symptom A**, the letter fragments.
- **Symptom B**, the narrative and imaging text. It needs an "is this an analyte?" gate on the model extractor.
- **The remaining duplicates of symptom C**, which belong to #241.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a8b0eaabc6d4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.