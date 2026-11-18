# Issue

**Title:** fix(devices): nap scores, WHOOP zones, breathing disturbances

## Description

Stacked on #213 (base `fix/nightly-sleep-and-distance`); retarget to `main` once #213 merges. Three defects in the same decoders, one commit each, each with a regression test that fails without it.

**1. A nap replaced the night's sleep scores.** WHOOP and Oura score a nap under the night's efficiency, performance, consistency and disturbance fields, and an afternoon nap falls in the night's 18:00 day. These now come from the main sleep only, #213's rule (WHOOP `nap` not true; Oura `type` `long_sleep` or absent). The catalogue has no nap score (only `napDuration`), so a nap's is not filed.

**2. Each WHOOP zone summarised to the whole workout.** The zone minutes carry the workout's span, which is right; the rows had a sleep stage's shape (`session/duration_union`). They are now `cumulative/sum_delta`, like the same workout's `activeCalories` and `exerciseDistances`. `TERMINOLOGY_VERSION` 1.5.10.

**3. Breathing disturbances were filed as awakenings.** open-wearables' `sleeping_breathing_disturbances` is Apple's `appleSleepingBreathingDisturbances` relayed (its SDK `metric_types.py`; Apple is the only provider on its coverage page), mapped to `sleepDisturbances` (103211-9 Number of awakenings). Apple says the metric is not an AHI and `apple.tsv` already declines it. Now an explicit decline.

| case (`series.aggregate` on decoded facts) | before | after |
|---|---|---|
| WHOOP efficiency, night 91 + nap 80 | last 80, avg 85.5 | 91 |
| WHOOP disturbances, night 12 + nap 1 | total 13 | 12 |
| Oura efficiency, night 93 + `sleep` 85 + `late_nap` 85 | last 85, avg 87.67 | 93 |
| WHOOP zones 20 / 10 / 1 min in a 60 min workout | 60 / 60 / 60 | 20 / 10 / 1 |
| plus a second workout, 15 low-zone min | low 90 | low 35 |
| open-wearables breathing disturbances = 4 | `sleepDisturbances` 4 | not filed |

Rows already stored are not rewritten. `data_type`, `window` and `aggregation_methods` are unchanged for every row touched.

**Checks:** ruff 0, compileall ok, lint-imports 6 kept / 0 broken, bare-interpreter import ok; pytest 1205 passed, 118 skipped, 12 xfailed. Merges cleanly with #214 (`instant/last` for the four scores; both set `TERMINOLOGY_VERSION` 1.5.10); on the merged tree its tests and these pass together.

Not changed here, from #213: the `provider-guide.md` coverage matrix still says WHOOP 26 (generated: 28), and the shipped WHOOP/Oura samples still expect pre-#213 names.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4e46991024fa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.