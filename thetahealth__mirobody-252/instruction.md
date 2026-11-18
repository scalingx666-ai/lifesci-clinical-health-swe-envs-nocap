# Issue

**Title:** resolver: a name with 测定 or a flag after it codes like the bare name

## Description

Part of #234: point 1 (`名称(缩写)测定`) and point 2 (new words). Point 3's hematocrit item went in with #248. Point 3's RDW-SD item is left as it is; see the last section.

### Point 1: `测定` and flag marks

A Chinese checkup prints the assay word, or a flag, after the analyte. None of these resolved, while the bare name did:

- `尿酸(UA)测定`
- `丙氨酸氨基转移酶(ALT)测定`
- `低密度脂蛋白胆固醇测定`
- `γ-谷氨酰基转移酶*`

Each therefore became an uncoded local series beside the coded one. `split_trailing_parenthetical` only fires when the bracket ends the name, and `测定` comes after it.

As the reply on the issue asked, the fix is a rule in the coding path rather than one override row per name. `OfflineResolver.resolve` now strips a trailing `测定` (or `測定`), `*`, `↑` or `↓` with `lexical.strip_report_marks`, and answers the result exactly as the bare name would be answered.

- **Only after a miss.** It runs after the name as printed has missed, so it can only turn a miss into a hit; every name that resolves today keeps its answer.
- **Every rule still applies.** It recurses through `resolve()`, so the stripped name meets the same rules as the bare one:

| Printed | Before | After |
|---|---|---|
| `尿酸(UA)测定` 420 umol/L | uncoded | 14933-6 |
| `丙氨酸氨基转移酶(ALT)测定` 30 U/L | uncoded | 1742-6 |
| `天门冬氨酸氨基转移酶(AST)测定` 25 U/L | uncoded | 1920-8 |
| `低密度脂蛋白胆固醇(LDL-C)测定` / `低密度脂蛋白胆固醇测定` 2.5 mmol/L | uncoded | 22748-8 |
| `总胆固醇(TC)测定` / `甘油三酯(TG)测定` / `尿素(Urea)测定` (mmol/L) | uncoded | 14647-2 / 14927-8 / 22664-7 |
| `γ-谷氨酰基转移酶(GGT)测定`, `γ-谷氨酰基转移酶*` 28 U/L | uncoded | 2324-2 |
| `血脂测定` | uncoded | refused, the category block |
| `血糖(HbA1c)测定` | uncoded | refused, two analytes, both codes named |
| `测定` alone | **41960-6, the type of an HbA1c measurement device** | refused (new `!unresolved` row) |

### Point 2: new words

These go in as override rows, with targets the index resolves:

- `体重指数BMI` → BMI
- `白球比例` → Albumin/Globulin
- `中性粒细胞比值` → neutrophils/leukocytes
- `红细胞分布宽度-变异系数` → RDW-CV
- `天门冬氨酸/丙氨酸氨基转移酶` → AST/ALT, 1916-6, from the issue's table

The trailing `*` on `γ-谷氨酰基转移酶*` is handled by the rule above, not by a row.

### Not in this PR

- **RDW-SD.** `红细胞分布宽度-标准差` abstains like `RDW-SD` and `红细胞分布宽度SD` already do. The overrides file records why: the 2.83 cut models RDW-SD as 115742-9, which carries no alias, so no row can reach it, and answering 30385-9 would put fL on the CV line. A reachable target needs the bundle build.
- **Uncoded Chinese names in general, and the Chinese display name.** That is #231's layer decision.

### Tests

- **`test_engine_coverage.py::READING_CASES`.** Nine cases, each asserting an exact code for a printed value and unit.
- **`test_a_report_mark_is_answered_as_the_bare_name_would_be`.** A category stays refused, two analytes stay two, `测定` alone is refused, and the RDW-SD row abstains.

All ten fail on `main`. The published score is unchanged at 347/347, because `READING_CASES` do not count toward it, so no README figures move. Every override row is still checked by the existing gate.

I also ran the maintainers' local resolver and lexical tests on `main` and on this branch: the failure set is the same.

```
pytest -q, minimal install ([test] only)            → 759 passed, 199 skipped, 12 xfailed
pytest -q, [app,test]                               → 1290 passed, 122 skipped, 12 xfailed *
pytest mirobody/tests/test_postgres_regressions.py   → 122 passed (PostgreSQL 17)
lint-imports → 6 kept · ruff → clean · comment style → 0 · versions → 1.5.10 · PHI lint → clean
```

\* Run locally without the two modules that need `quickjs_rs`; CI installs it.

`docs/standardization.md` and its Chinese edition describe the new step; there is no Japanese edition of that page. Readings already stored under these names move to their codes with `mirobody recode`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7c7dc1bd0f41`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.