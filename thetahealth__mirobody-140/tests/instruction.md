# Issue

**Title:** Add Turkish lab-report spellings to resolver overrides

## Description

Follows Discussion #137, using #88 as the template.

- resolver_overrides.tsv: `Total Kolesterol` -> Cholesterol, `HDL Kolesterol` -> HDL-C, `Trigliserit` -> Triglyceride, `Glukoz (açlık)` -> the fasting glucose key. Before this, the first three resolved to nothing and the fourth landed on plain glucose (2339-0) with the "fasting" qualifier lost.
- test_engine_coverage.py: one case each, with must-not patterns (HDL vs total cholesterol, fasting vs plain glucose).
- test_cross_language_identity.py: `Total Kolesterol` added to the total cholesterol row.
- CHANGELOG.md: one line under Unreleased.

Ran: pytest -q mirobody (362 passed, 13 xfailed), ruff check mirobody examples, lint-imports. With the TSV rows stashed, the four new cases fail.

I looked up codes 2093-3, 2085-9, 2571-8 and 1558-6 on loinc.org (all Active). Spellings: taken from the examples in Discussion #137.
I used Claude to draft the rows and tests and to review; the code checks above are mine.

Not covered: uppercase dotted İ ("KREATİNİN", "TRİGLİSERİD"). "İ".casefold() gives "i" + U+0307, so the lookup key differs from the index key (lexical.py ~line 85, resolver.py ~line 321). Left for the engine side, as discussed in #137.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `338d54f44a3d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.