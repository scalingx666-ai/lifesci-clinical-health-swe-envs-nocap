# Issue

**Title:** bench: score phrased absence and continued labels; name docs by date

## Description

Stacked on #174 (`c5896387`); merge that first. Once it lands, this PR shows only its own commit.

The harness100 scorer failed correct answers it could not parse, and 32 questions named corpus files that the product's `/library/` renames.

- Absence, uncertainty, coverage and which side of a bound a value falls on are now matched as phrases (`words` facts gain `patterns`).
- A value binds to its label across a continuing clause, a list item, a table cell, or worked arithmetic. Another test's name stops that.
- Document questions accept the file's stored readings, as lab questions already do.
- Also: drug short names, a year-less month-day, and questions that name documents by type and date.
- Suite `harness100-20261023b`. Gold and the loaded record are unchanged, so the existing accounts work.
- Each class has red-then-green cases, with negatives, in `tests/agent/test_local_eval_contract.py`.

On the no-hint pilot's reviewed transcripts, 39 of 40 scorer false negatives now pass, with no new false positives. Details are kept internal.

Gates: ruff, compileall, pytest (856 passed / 107 skipped / 12 xfailed), lint-imports 6 kept / 0 broken, bare library import, `cases.py --check`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aef49c5ce81b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.