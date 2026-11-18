# Issue

**Title:** catalog: accept every unit LOINC declares for a property (14.9% → 38.1%)

## Description

## What

The catalogue covered **226 of LOINC's 1,519 Universal Lab Orders (14.9%)**. This takes it to **578 (38.1%)** — and the fix is a two-line change in the *unit gate*, not more vocabulary.

## Why it was stuck

`standardize_build/loinc_catalog_rows.py` decided whether a generated row's unit could express the code's PROPERTY by a hand-written table that only knew the units the first batch happened to use. LOINC declares more per property:

```
k[IU]/L   [arb'U]/mL   m[IU]/mL   ...
```

Those orders were dropped as *"unit does not match PROPERTY"* — 217 good rows — while the vocabulary to answer them had been present all along.

## The fix

The repository already carries the PROPERTY family of every UCUM unit it understands — `mirobody.units.families`, which `test_unit_families_vs_loinc.py` guards against the LOINC release. The gate now accepts the **union** of the two sources:

```python
if unit not in PROPERTY_UNITS[prop] and prop not in unit_families(unit):
    reasons[f"unit {unit} does not match PROPERTY {prop}"] += 1
    continue
```

A unit still has to name this code's own property — nothing is loosened. The hand-written table is **kept, not replaced**: three of its entries deliberately disagree with the general mapping.

## Result

Same generator, six-axis check and naming rules unchanged:

| | before | after |
|---|---:|---:|
| rows generated | 146 | **352** |
| universal orders covered | 226 / 1,519 (14.9%) | **578 / 1,519 (38.1%)** |
| catalogue codes | 304 | **639** |

Audit of every added row:

- **352/352** displays resolve back to their own code
- **352/352** units agree with their code's PROPERTY
- **0** member-name collisions

## Still excluded, by design

| count | reason |
|---:|---|
| 343 | `PROPERTY = PrThr` — presence/absence needs a `data_type` the catalogue does not model |
| 79 | presence/identity (`Prid`) |
| 69 | `EXAMPLE_UCUM_UNITS` the normalizer does not recognise |

## Test change

`test_each_unit_matches_its_code_property` asserted against a fixed unit table, which would have rejected every newly admitted unit. It now falls back to `unit_families(unit)` for units the table does not name — the same authority the generator reads, so the test and the generator cannot drift apart.

## Verification

- `pytest -k "unit or standardize or translate or catalog or resolver or engine or loinc or universal"` → **263 passed, 13 skipped**
- `ruff check mirobody examples benchmarks/windows` → clean
- coverage measured against the LOINC 2.83 release's `LoincUniversalLabOrdersValueSet`

## Provenance

The gap analysis came from a survey of LOINC 2.83's unused assets, which found the vocabulary already complete: **1,223 of the 1,293 uncovered orders were already resolvable** — the missing piece was catalogue rows, and the rows were being rejected by this gate. The report (including why `RELATEDNAMES2`, `PartFile` and the linguistic variants add almost nothing, and why VSAC/UMLS/CDISC do not fit an offline-reproducible build) is in the workspace docs.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2f0b0eeb47b9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.