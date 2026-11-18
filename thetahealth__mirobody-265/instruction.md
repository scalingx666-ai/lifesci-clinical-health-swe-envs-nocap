# Issue

**Title:** journal: name a LOINC-coded entry in the reader's language

## Description

## Summary

 (#256/#259), found in the 1.6.0 release testing. The journal (数据 › 记录) was not part of that work: on a Chinese page, after logging "昨晚开始头疼，血压150/95，没发烧，二甲双胍500mg早晚各一次", the cards read `收缩压 150 mmHg → Systolic blood pressure 8480-6`. `GET /api/v1/journal` and the `POST`s that log to it sent only `display`, LOINC's long name.

- **Server** (`journal_router._named`): a LOINC-coded entry gets `label` from `standardize.label_for` in the request's language, the one name #278 gives a code in `GET /api/v1/health-indicators` and the model's table. It applies to the list, to `POST /journal/sentence`'s `written`, and to `POST /journal`. `display` is unchanged.
- **ICPC-3 decision:** a complaint gets **no** `label` in any language and keeps WONCA's English preferred term (头疼 → `Headache NS01`). The bundle has no Chinese ICPC-3 title (`res/icpc3/icpc3.NOTICE`: the `symptoms_zh.tsv`/`conditions_zh.tsv` files map patient phrases to codes and hold no ICPC-3 term), WONCA licenses translations separately, and CC BY-ND forbids publishing our own. If a licensed Chinese ICPC-3 is ever obtained, the label goes in the same `_nam- **Web client:** thetahealth/mirobody-web#27, already in main's `frontend/` (built from mirobody-web `199e9e4`), so this PR no longer carries a bundle of its own.
hes.
- Docs: `docs/standardization.md` §7 and its Chinese edition say what the journal names; CHANGELOG Unreleased has the entry.

| | 中文 page | English page |
|---|---|---|
| 收缩压 150 mmHg (8480-6) | `"label": "收缩压"` → **收缩压** | no `label` → Systolic blood pressure (as before) |
| 舒张压 95 mmHg (8462-4) | **舒张压** | Diastolic blood pressure (as before) |
| 心率 72 (8867-4) | **心率** | **Heart rate** (LOINC's consumer name) |
| 头疼 (NS01) | Headache | Headach## Merge order

Updated 2026-11-10 onto main `80246c58` (after #278): merged main in, took main's `frontend/`, and moved `_named` onto `standardize.label_for` (114ae40b), so the diff against main is the journal change alone. It goes out in 1.6.1; merge it before the release PR.

it.

## Testing

- 2026-11-10, on 114ae40b: ruff, compileall, comment style, PHI lint, `lint-imports` (6 kept, 0 broken); full suite against PostgreSQL 17: 1654 passed, 12 xfailed.
- `ruff check mirobody examples`: clean. `python -m compileall -q mirobody`: ok. `lint-imports`: 6 kept, 0 broken. Bare-interpreter import of `mirobody.kernel.meds, mirobody.kernel.query`: ok.
- `pytest -q` (this worktree, local suite): 1461 passed, 143 skipped (no `MIROBODY_TEST_POSTGRES_DSN`), 12 xfailed. New in `mirobody/tests/test_zh_names.py`: both routes (`list_entries`, `log_sentence`) run with the database and the text model stood in for. `label` is 收缩压/舒张压/心率 for zh-CN, absent/absent/`Heart rate` for en, and absent on the ICPC-3 entry in both. The zh and en cases fail on the unfixed router. `test_frontend_bundle.py` passes.
- Live: own Postgres + `mirobody serve` from this branch + the local MiniCPM5-2B router for the sentence model, in the built-in browser. On 简体中文, the sentence above gave outcome cards `收缩压 150 mmHg → 收缩压 8480-6`, `舒张压 95 mmHg → 舒张压 8462-4` and `头疼 → Headache NS01` (tooltip on the label: the English name), and the feed showed the same. `fetch` with `X-Language: zh-CN` vs `en` returned `label` only on the two zh readings. Switching to English in Settings refetched the feed, which read as before. The e2e harness (`scripts/e2e_health_data.py`) was not run: the change adds a read-side field and no SQL.

## Not covered

- The outcome list under the composer is the `POST`'s own answer for the sentence just logged, so it keeps the language it was logged in after a language switch, until the next entry or ×. The feed below it does rename.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0d9c88c43e89`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.