# Issue

**Title:** query: name each series once and write each number one way

## Description

The same change as #277, which was merged into `fix/aggregate-series-names` after #270 had merged, so it never reached `main`. This PR brings it to `main`, on top of #269's per-series blocks.

## What was wrong

What `query_health_indicators` returned for an indicator was not one thing per series, so it could not be made shorter without losing track of what each row was. Measured on a fixture of a US panel in mg/dL, a Chinese panel in mmol/L and device sleep and heart-rate data:

- **Three names for one series.** A raw row carried LOINC's long name (`Cholesterol in LDL [Moles/volume] in Serum or Plasma`), the label (`LDL cholesterol, Blood`) and what each report printed (`LDL Cholesterol`, `低密度脂蛋白胆固醇`). The last one is the source's own data; since #271 the printed value, unit and range stay out of the model's context, but the printed name did not.
- **A device series read as its key.** `dailyDeepSleepPercentage` had no label, although every one of the 893 device metrics in `kernel.metrics` has a readable name (`Daily Deep Sleep Percentage`, 深睡比例).
- **Numbers were unrounded and differed by view.** A converted reading was `5.48` in raw rows and `5.482994956679169` in a month; a mean of 3.57 and 3.10 was `3.33455967929652`; a device export's `21.916666666666668` passed through. Only trend rounded (six significant figures).

## What changed

- `standardize.label_for(system, code, language)` is the one name a reader sees: `names_for` for a LOINC code, the catalogue label for a device metric (Chinese from `res/catalog/labels/zh.tsv`, otherwise its English display).
- Every reading of a series carries the series' identity (name, code, unit) in every view, except a reading whose unit does not convert, which keeps the code that says what that unit measures. A reading's own code stays in `printed.code`.
- The printed name moves into `printed.name`, beside the printed value, unit and range. The records list, `GET /api/data` and the export keep it as `name`. Reported entries keep their words as `name`.
- `query.shown_names` decides the one name the model reads: the label, or LOINC's long name where a series has none or two series in one answer share a label (whole-blood and serum glucose are both 葡萄糖). The table and every note that names a series (trend, units that do not convert, unverified sources, outside the window, held elsewhere, banded stats) use it. The `label` and printed-name columns leave the model's tables.
- `_by_names` accepts that name as a selector: names the exact match leaves unmatched are tried against each series' label in the request's language and in English, so the name the model reads is a name it can ask by.
- `query.presentable`, applied once the service has its rows (after trend has computed from unrounded daily values): computed values (min, max, mean, median, spread, change, a sum that is not a whole number) to six significant figures, as trend already did; whole-number sums untouched (1,234,567 steps stays exact); a reading's float noise (more than six decimals) cut to six significant figures, its text kept in `printed`.

REST rows (`GET /api/v1/health-indicators`) change the same way. `indicator` there is still LOINC's long name, which the web's drawer selects by; the web reads `label` where there is one, so device metrics show their readable name there too. The web does not read a reading row's `name` (checked against mirobody-web `main`).

## How to tell

The same fixture, characters the model reads (table only), on `main` with #269's per-series blocks and with this change on top:

| view | main | this PR |
|---|---:|---:|
| catalog | 712 | 577 (−19%) |
| raw | 2,091 | 1,716 (−18%) |
| latest | 1,023 | 769 (−25%) |
| stats | 1,399 | 1,038 (−26%) |
| month | 774 | 424 (−45%) |
| day | 919 | 817 (−11%) |
| trend | 1,184 | 1,116 (−6%) |

```
(constants: indicator=LDL cholesterol, Blood, unit=mmol/L, system=http://loinc.org, code=22748-8)
time|value|ref|file
2026-06-20 09:00:00|3.10|<3.37|synthetic-cn-lab
2025-03-10 09:00:00|3.57|<2.59|synthetic-us-lab
```

`view=raw` over a mixed panel shows `LDL cholesterol, Blood` and no `LDL Cholesterol`; `view=stats` has no number longer than six significant figures.

## Tests

- New database case `test_the_model_reads_each_series_once_and_nothing_the_report_printed`, in English and Chinese, over `raw`, `latest`, `stats`, `day`, `month` and `trend`. It asserts that each series is named once and the same way in every view; that no printed name, unit or value reaches the model's text; that no number runs past six figures; that the device series reads as its label (`Daily REM Sleep Percentage` / `REM睡眠比例`); and that asking again by each shown name returns exactly that series. Each condition is visible in the same fixture rendered on the base branch.
- `test_zh_names.py`: the label-column test now asserts one name per series, including two series that share a label.
- Updated expectations: #271's `printed` now includes `name`; #270's cross-view test compares the names the model reads; #269's `test_one_row_per_series_is_one_table` expects the catalogue named by its labels with no `label` column; `tests/agent/tools/test_stats_output.py` expects `stddev=4.3589`.
- `query.shown_names` is keyed by #269's `query.series_key`, so the blocks and the names group rows the same way.
- Full suite with `MIROBODY_TEST_POSTGRES_DSN` set (disposable PostgreSQL 17), on the merge with `main`: 1650 passed, 12 xfailed, 0 skipped.
- `ruff check mirobody examples benchmarks/windows`, `scripts/check_comment_style.py`, `python -m compileall -q mirobody`, `lint-imports` (6 kept, 0 broken), `scripts/check_versions.py`, the PHI log gate and a bare library-layer import: clean. Not run locally: the minimal-install job and the packaging steps.

## Not in this PR

- Stats `min`/`max` are computed values (`5.48299`) where the raw row shows the printed `5.48`; writing them as the readings were printed is a follow-up.
- `system` is still a URL on every row, `reason` can read `engine:no-match`, and trend notes restate each series that has too few points.
- The web's Indicators tab was not checked in a browser.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d4d754aba29f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.