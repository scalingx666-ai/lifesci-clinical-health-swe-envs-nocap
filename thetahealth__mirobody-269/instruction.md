# Issue

**Title:** feat(agent): one compact table per indicator in a mixed result

## Description

## What

A readings result that **mixes indicators** kept `indicator`, `unit`, `system`, `code` and `file` on every row. They differ *across* indicators, so `query.compact` cannot hoist them — yet each is constant *within* one. The model re-read the same five values on every row.

This renders **one compact table per indicator** instead. Each block hoists its own constants through the existing `query.compact`, so only the genuinely varying columns (`time`/`period`/`count`/`value`) stay in the table.

## Before / after

Before (two indicators, 8 columns, six constants repeated per row):

```
indicator|time|value|unit|ref|system|code|file
glucose|2026-01-01|5.1|mmol/L|3.9-5.5|LOINC|2339-0|watch.csv
glucose|2026-01-02|5.2|mmol/L|3.9-5.5|LOINC|2339-0|watch.csv
steps|2026-01-01|8000|count||LOCAL|steps|phone.csv
steps|2026-01-02|8001|count||LOCAL|steps|phone.csv
```

After (same four rows, same information):

```
(constants: indicator=glucose, unit=mmol/L, ref=3.9-5.5, system=LOINC, code=2339-0, file=watch.csv)
time|value
2026-01-01|5.1
2026-01-02|5.2

(constants: indicator=steps, unit=count, system=LOCAL, code=steps, file=phone.csv)
time|value
2026-01-01|8000
2026-01-02|8001
```

## Why (measured, not asserted)

Paired benchmark: same questions, same model, **only the rendered table changes** (n=100, per-item pairing, exact McNemar).

| table | columns | accuracy (Qwen3.5-2B) | vs baseline | discordant | p |
|---|---:|---:|---:|---:|---:|
| full | 7 | 60.0% | — | — | — |
| + one *per-row-varying, task-irrelevant* column | 8 | **50.0%** | **−10.0pp** | 13:3 | **0.021** |
| + one *constant, task-irrelevant* column | 8 | 54.0% | −6.0pp | 11:5 | 0.21 |
| + *relevant* information (real dates instead of day index) | 7 | 65.0% | +5.0pp | 9:14 | 0.40 |
| slim (drop the four constant/empty columns) | 3 | 63.0% | +3.0pp | 9:12 | 0.66 |

Two things follow. Prompt length is not what matters (+4.4% cost 10 pp; +10.5% gained 5 pp) — what matters is whether a column is **relevant to the question** and **varies per row**. And dropping the irrelevant ones showed no detectable loss: 63.0% vs 60.0% on the 2B, 94.0% vs 91.0% on a teacher-level hosted model, with the prompt roughly halved.

**Read that as "no detectable loss", not "proven harmless"**: at n=100 a paired design needs roughly a 12–14 pp effect for 80% power, so a 3 pp regression would not have shown up. For a product decision that is still enough — the change is a strict token saving and the point estimates move the right way — but a paper would need n≥300 or an equivalence test (TOST) to claim non-inferiority.

`query.compact` already gets this right for whole-table constants; the gap is the columns that are constant *per indicator* only. The closest published work is PieTa ("Piece of Table", ACL 2026), which prunes a table to question-relevant rows and columns for +2–5 pp on the same reader; it selects by relevance, so a redundant column that a relevance filter would keep (a unit column) is exactly the case it does not isolate.

## Tests

- New `mirobody/tests/test_render_indicator_blocks.py` (4 cases): single indicator unchanged, mixed indicators produce one block each, no cell lost, blank indicator still groups.
- `pytest mirobody/tests`: **881 passed, 111 skipped, 12 xfailed**.

## Two questions for the maintainer

1. **Row order**: grouping makes each indicator's rows contiguous, so a cross-indicator chronological view is no longer one table. If "all indicators aligned by time" is the common case, this can be changed to sort by time and still block per indicator.
2. **`system`/`code`**: the existing comment says both must ride with a value or the model fills the code in from memory. They are still present here — once per block instead of once per row. If there is a worry that a small model misses block-level constants, gate the grouping on `len(rows) >= N`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `818b87a61470`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.