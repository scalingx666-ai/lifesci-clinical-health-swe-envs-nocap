# Issue

**Title:** standardize: keep the official names LOINC actually prints in the index (50 → 120 char keys)

## Description

## What

The alias index capped a key at **50 characters**. That cap came from the index this replaces, and it silently dropped the designation a lab report actually prints for a result.

Of the **287 codes** `res/catalog/metrics.tsv` carries, **81** have an official long name longer than 50 characters:

```
Lactate dehydrogenase [Enzymatic activity/volume] in Serum or Plasma by Lactate to pyruvate reaction   (112)
Alanine aminotransferase [Enzymatic activity/volume] in Serum or Plasma                               (86)
```

None of those 81 names was a key. A name that is not a key cannot answer — and it cannot serve as an override target either, which is why the name-history aliases prepared for this catalogue could only ship **14 of 425** rows.

The cap is **120** now, above every laboratory designation in LOINC 2.83. The classifier-word cap (`DF_CAP 500`) still refuses anything that names hundreds of codes, and the CJK/Latin minimums are unchanged.

## Measured on the catalogue, rebuilt bundle

| | before | after |
|---|---:|---:|
| long common name recall | 73.9% | **99.3%** (285/287) |
| short name recall | — | **99.3%** (285/287) |
| official long names that are keys | 206 | **287** |
| codes whose long name was missing | 81 | **0** |
| historical names that resolve | 721 | **1,128** of 1,159 |

The historical names matter on their own: a report printed under a code's old wording — `Lactate Dehydrogenase (LDH), Blood` — now finds the code, so the **425-row override table** that was going to be needed for them is unnecessary. Adding those rows would have been the wrong fix twice over: they only papered over a truncated key, and 411 of them pointed at targets that existed *only* because of the override table itself.

`COMPONENT` recall stays at 65.5%, which is not a regression: a bare component ("Glucose") is genuinely ambiguous across specimens, and refusing it is the correct behaviour.

## What it does *not* change

Measured on the three real corpora, the rebuilt bundle resolves exactly the same names as before:

| corpus | old bundle | rebuilt |
|---|---:|---:|
| NHANES 2017-18 (192 printed names) | 58 (30.2%) | **58 (30.2%)** |
| ESL-Bench (722) | 102 (14.1%) | **102 (14.1%)** |
| WearableQA (33) | 16 (48.5%) | **16 (48.5%)** |

Which is the honest description of the fix: these corpora print consumer and vendor wording ("Fasting Blood Glucose-FBG"), not LOINC's own designations, so the long-name keys do not reach them. **No regression, no gain there.** The gain is where a report prints the standard's own wording — long common names, short names, and the names a code carried before its current one.

## Bundle

`fhir_loinc_bundle.tar.gz` is rebuilt from LOINC 2.83 (`loinc-2.83+2026.10.27-126ecba69782`), **12.7 → 17.1 MB**: the +4.4 MB is the long names that were being discarded. The `NOTICE` version line moves with it.

## Verification

- `pytest -k "unit or standardize or translate or catalog or resolver or engine or loinc or universal"` → **263 passed, 13 skipped**
- `ruff check mirobody examples benchmarks/windows` → clean
- Recall figures computed against `Loinc.csv` (287 ACTIVE catalogue codes, LCN/SHORTNAME/COMPONENT fields)

## Note for review

The diff is small in code (one constant) and large in data (the LFS bundle). The measurement that matters is the recall table above; the bundle is reproducible with:

```
python -m standardize_build.build_bundle --loinc <unpacked Loinc_2.83> --date 2026.10.27
```
(~16 minutes)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2f0b0eeb47b9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.