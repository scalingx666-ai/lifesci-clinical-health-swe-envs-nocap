# Issue

**Title:** extraction: a scanner's settings and a history heading are no reading

## Description

Part of #235 (symptom A, and the heading half of symptom B).

### What was wrong

Chinese check-up PDFs left rows in the indicator list that are not readings of the person:

- **A:** `AO%`, `D`, `DR`, `FR`, `Frd`, `Frq`, `Gn`, `PAT TIS`, `S/A`. These are the settings an ultrasound scanner prints beside its image (gain, depth, frame rate and so on). The model is not the only reader that stores them. Given `| FR | 25 | Hz |`, `| Frq | 3.5 | MHz |`, `| D | 16 | cm |` and `| Gn | 50 | |` in a table, the strict table rules read all four as `laboratory` rows. The issue traced the narrative rows to the model path, which has no such gate. The rules path has none for these rows either.
- **B:** `既往史` and `其他` are a history heading and a form's catch-all heading. No `detection_method` makes them right.

**Why not a length rule or the vocabulary.** A length rule is out: `K`, `Na` and `Ca` are analytes. The vocabulary cannot be the test either, because it resolves `K`, `Na`, `HR`, `RV5`, `SV1` and `FR` the same way, to nothing.

### Change

- `indicator_extractor.NOT_READINGS` is a closed list of labels, compared by `standardize.name_key`, so `ＦＲ` and `既往史：` match. It holds:
  - the nine scanner labels from the issue;
  - the history headings of an admission record as 《病历书写基本规范》(2010) lists them (主诉, 现病史, 既往史, 个人史, 婚育史, 月经史, 家族史);
  - `其他` / `其它`.
- `read_indicators` drops matching rows after the rule rows and the model rows are merged, so both readers pass the same gate. The frozen answer keeps them, as read.
- The log line gains `not_a_reading_count`. It carries no names and no values.
- The comment on the list names the look-alikes that must not be added, because they are readings: an echocardiogram's `AO` and `E/A`, and `MAP`.

### Symptom B: which statement was right

The reply on the issue said "already stored correctly … a display fix". PR #251 said B "needs an 'is this an analyte?' gate on the model extractor". From the code, each is right about different rows:

- **Organ rows** (`心影`, `两肺纹理`, `气管及诸纵隔`, `双肾`, `双肾结晶`) are findings by design. The prompt asks for one finding per organ, and `indicator_store` stores an Imaging or Pathological row as `kind='finding'`. The test now pins this. Every catalogue row carries `kind`, but the web client's Indicators panel never reads it: no source file under `src/pages/Indicators` uses a catalogue row's `kind`, so findings are listed with the lab analytes. That half is a display fix in the client and is not in this PR.
- **Headings and history** (`既往史`, `其他`) are neither measurements nor findings. They need the gate, and this PR adds it.
- **A gap neither statement covered.** `kind` comes from the model's `detection_method` alone, and none of the schema's five methods fits a physical or dental examination. So `牙周` and `义齿` are findings only if the model calls them Imaging. Adding a method needs a guard that keeps a number a measurement, because a finding's record carries text, never a number. This is recorded in `docs/roadmap.md` together with the display half, and so is the one ultrasound sentence that came out as three rows (`双肾彩超`, `双肾`, `双肾结晶`).

The ECG rows of symptom A (`HR`, `RV5`, `SV1`) are kept. Their missing panel context, and the doubled `RV5`/`SV1`, are not addressed here.

Rows already stored stay until their report is read again. `POST /api/v1/data/reprocess-file` (#279) erases them first.

### Test

`mirobody/tests/test_extraction_regressions.py` uses synthetic values under the printed names from the issue:

- `test_scanner_settings_and_record_headings_are_not_readings` mocks the model's reader. It drops the nine scanner labels, `ＦＲ`, `既往史`, `既往史：` and `其他`, and keeps `K`, `Na`, `Ca`, `HR`, `RV5`, `SV1`, `AO`, `E/A`, `MAP` and all eight organ rows, in order.
- `test_the_table_rules_rows_pass_the_same_gate` runs a markdown table through the rules with no model call and keeps only `K` and `Na`.
- `test_an_imaging_row_is_stored_as_a_finding` checks that `心影` and `双肾结晶` (Imaging) are stored as `finding`, and `HR` and `K` as `measurement`.

With the gate disabled, the first two fail and the third passes; it pins existing behaviour.

On this branch, rebased on current `main`:

```
pytest -q, [app,test], no PostgreSQL → 1495 passed, 168 skipped, 12 xfailed
ruff → clean · compileall → ok · lint-imports → 6 kept, 0 broken
bare library import → ok · comment style → 0 · PHI lint → clean · versions → 1.6.0
```

The 168 skips are the database cases (`MIROBODY_TEST_POSTGRES_DSN` unset). I did not run the end-to-end script against a live stack.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f8fbd7610cb4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.