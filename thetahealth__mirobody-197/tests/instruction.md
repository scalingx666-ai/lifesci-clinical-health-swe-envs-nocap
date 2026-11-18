# Issue

**Title:** collect: a keyword search keeps every series that shares a name

## Description

## Why

A keyword search could not reach a series whose name another series also used. `PostgresHealthQuery._by_keywords` kept one series per printed or display name:

```python
by_label.setdefault(label, sid)
```

Several series of one analyte are expected to coexist. Device readings keep their own namespace (`mirobody-device:<name>`) rather than the lab's LOINC code, so a lab fasting glucose and a CGM fasting glucose printed under the same name are two series, and the second one was dropped. Asked "what fasting glucose did my CGM record on 2024-08-21?", the agent said there was none, with 1,007 CGM readings stored (6.949 that day).

## What changes

- A matching name now brings every series filed under it. The rows the search returns already carry `series`, `file` and `modality`, so the agent can tell them apart.
- `MAX_KEYWORD_NAMES` still caps the result. It already counted series.
- The same question is now answered with the CGM's 6.95 and the same-day lab value 7.45, and the agent explains why they differ.

## Verified

On `36fbbe8`, `pip install -e '.[app,test]'`:

- Two regression tests fail on `main` and pass here: a unit case in `test_collect_regressions.py`, and a PostgreSQL case in `test_postgres_regressions.py` (a lab and a device "Glucose" become two series; one keyword search finds both).
- pytest with `MIROBODY_TEST_POSTGRES_DSN`: 1277 passed, 3 skipped, 12 xfailed.
- `benchmarks/genomics` and `benchmarks/health_records` unittest suites: OK.
- Ruff, compileall, six import contracts, bare library imports, comment style, version check and PHI baseline: pass.
- End to end, a local server of `main` with and without this change. The database was seeded with the 20 ESL-Bench synthetic users, lab results and device data loaded as structured data. Default chat model `anthropic/claude-sonnet-5.5`. On 86 questions comparing a lab value with that day's device value:
  - `main`: 22 correct; 32 answers gave no device value.
  - this change: 86 correct; every answer gave the device value.

  Values stated in each answer were extracted by a separate model and compared in code with the stored data. Nine further questions about lab and device trends are left out: their key compares 7-day device windows that the question does not name.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9df0c3850b0d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.