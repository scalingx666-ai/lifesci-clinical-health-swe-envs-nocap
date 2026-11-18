# Issue

**Title:** fix(catalog): summarise a sleep score to its value

## Description

`sleepEfficiency`, `sleepPerformance`, `sleepConsistency` and `sleepDisturbances` are one figure a vendor computes for one sleep, but the catalogue gave them a sleep stage's shape (`session`/`duration_union`). `series.aggregate` ignored the value and returned the minutes the sleep spans. This makes them `instant`/`last`, the shape `sleepQuality` already has.

Measured end to end (decode, write, daily aggregation, query) on PostgreSQL 17:

| | Before | After |
|---|---|---|
| `series.aggregate`, WHOOP efficiency 91% / performance 88% / consistency 76% / disturbances 12 | 480 min each | 91% / 88% / 76% / 12 |
| `series.aggregate`, Oura efficiency 93% / restless periods 3 | 450 min each | 93% / 3 |
| `series.aggregate`, a count with no span | nothing | 4 |
| WHOOP re-scores a night, 89% then 91% | 480 min | 91% |
| `series_data`, `dailyAvgSleepEfficiency.*`, `dailyTotalSleepDisturbances.*`, query layer | — | identical |

**Why `last`.** When a sleep is re-scored, `last` and `provider_value` keep the newer score, while a mean or a sum blends old and new. Only `last` gives the same answer whatever order the sleeps synced in. `provider_daily` means one figure a day, but WHOOP and Oura score naps under these names too; the daily figure already has its own name, `dailySleepEfficiency`.

**Stored data.** Unchanged. `data_type`, `window` and `aggregation_methods` are untouched, so readings land in the same table on the same day under the same daily names. `TERMINOLOGY_VERSION` goes to 1.5.10 because `state_class` and `aggregation_policy` are identity fields.

**Test.** `mirobody/tests/test_sleep_scores.py` checks each vendor's figure and the re-score. It also fails any `duration_union` row whose unit is not a time. All five cases fail on main and pass here. The full suite with a database: 1314 passed, 12 xfailed; ruff, compileall, `lint-imports` (6 kept) and the bare-interpreter import are green. The change merges cleanly with #213, and both PRs' tests pass on the merged tree.

**Not in this PR** (decoder work, after #213): a nap's scores still replace the night's on the same 18:00 day; each WHOOP workout zone summarises to the whole workout's length; and Open Wearables files breathing disturbances as awakenings.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2b2831dddf34`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.