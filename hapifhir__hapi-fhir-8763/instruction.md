# Issue

**Title:** Replace jscience with org.fhir:ucum for number search parameter day normalization

## Description

`jscience` (4.3.1, unmaintained) is used only to convert UCUM time quantities to days for number search parameters, and `org.fhir:ucum` already ships. `jscience` and `javolution` leave the tree.

**For review: indexing behaviour changes**
- `d`, `wk`, `mo`, `a` and other UCUM time codes used to fail the write; jscience read `a` as "are". They now index in days: `a` is 365.25 d and `mo` is 30.4375 d.
- Non-time and unknown codes also used to fail the write. They now index unchanged, as the Quantity normalization does.
- `s`, `ms`, `min`, `h` and the non-UCUM names `day`, `week`, `month` and `year` are unchanged.
- jscience-only names such as `year_sidereal` now index unchanged, so a reindex changes those values.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `247833421129`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.