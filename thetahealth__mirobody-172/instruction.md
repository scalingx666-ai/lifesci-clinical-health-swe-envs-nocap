# Issue

**Title:** benchmarks: cover the chart and language dimensions with an extras generator

## Description

## What and why

Measured on `harness100-20261021` (`cases.jsonl`):

- **chart**: `chart: true` on **2 / 100** cases, so the `chart` check is free on the other 98;
- **language**: **en 60 / zh-CN 30 / ja 5 / zh-TW 5**, and per person p002 has 24 cases while p006 has 4;
- facts per case: 72% carry only 1-2 facts, so one number decides a case.

A model that never draws a chart, or only ever answers in English, still scores well on those checks. This PR adds a generator for extra cases rather than changing the maintained set.

## What is added

- `benchmarks/local_models/expand_cases.py` — builds extras in the `cases.jsonl` shape from a mirobody-gen build, with every answer computed from the build (never from product output). Families: device-latest, device-sum, device-count, weekly chart, journal-count, absence; each emitted in **zh-CN / zh-TW / ja / en**. Verified locally with a synthetic corpus; the exact count depends on how many people have a 30-day window.
- `benchmarks/local_models/README.md` — a section documenting the coverage gap, the generator, and how to run the extras (append to a *copy* of `cases.jsonl`, recompute the manifest hash, relax the exactly-100 rule **in that copy**) so the maintained suite keeps its provenance and baseline.
- `benchmarks/local_models/score.py` — an `efficient` observation (`tool_calls <= 8 and seconds <= 60`) recorded beside the checks. It is deliberately **not** part of `pass`, so historical comparisons stay valid.

## What is not changed

`cases.jsonl`, `plan.json` and the frozen suite are untouched: no baseline moves.

## How it was checked

```
python benchmarks/local_models/expand_cases.py --corpus <build> --out /tmp/extra.jsonl --people 2
# wrote 76 cases (charts 16); langs=['en', 'ja', 'zh-CN', 'zh-TW']; domains=['absence', 'device', 'journal']
```

The generated cases were then run through this harness locally via `--cases`, together with the `efficient` addition above.

## Review fixes (2026-10-23)

- Per-locale metric labels: `ja` and `zh-TW` no longer fall back to Simplified Chinese; `journal-count` is skipped in a locale when the symptom has no translation.
- `device-sum` is emitted only for additive metrics (`steps`); `rhr`/`weight` get latest/count/chart instead of a meaningless total.
- Tied journal symptoms use a deterministic `Counter` + sorted tie-break (verified across `PYTHONHASHSEED`).
- Extras carry their own `suite_id` so `score.py`'s subject check runs; `--as-of` is configurable.
- `efficient` records `None` when timing is absent instead of treating it as 0.
- Ruff clean; synthetic corpus check: locales correct, no weight/rhr sum, stable output.

## Second review fixes (2026-10-23, on the pinned harness100 build)

Main is merged in (for `cases.half_step`). Running the generator on the real build showed cases that were wrong as generated:

- **Questions named the corpus person.** For example, "请查询 p001 …". They are now first person.
- **Journal cases mixed languages.** Six of eight journals are Chinese, but the symptom table was keyed by English names. The zh/ja forms were skipped, and the English questions carried Chinese names. A journal case is now asked in its journal's own language, about a symptom written one way.
- **Days ignored the account time zone.** p006 is a UTC account with `+08:00` records, so 839 readings fell on another day. Days now come from `cases.device_series` in `plan.json`'s time zone. A window also skips days that have a loaded document reading.
- **Tolerances** now use `cases.half_step`. The old sum allowed ±0.2%, about 460 steps.
- **Absence** now uses `cases.NO_DATA` and also checks the loaded documents.

Result: `--corpus <harness100 build>` writes 140 cases (36 charts). Device, chart and absence cases come in all four locales; journal cases are zh-CN ×5 and en ×3. A contract test pins the time-zone, language and first-person rules. Gates: ruff, compileall, pytest (801 passed), lint-imports 0 broken, PHI lint and `cases.py --check` all pass. The PR merges cleanly with main and with #176.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aef49c5ce81b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.