# Issue

**Title:** fix: correct PDW lab value range from 150-520 to 9-17 fL

## Description

## Problem

The Platelet Distribution Width (PDW, LOINC 32207-3) observation in Synthea's module JSON files has an incorrect reference range of **150–520 fL**. These values appear to have been copied from the adjacent Platelet Count observation (LOINC 777-3, range 150–450 ×10³/µL), which is a completely different measurement.

According to published reference values ([PMC2843567](https://pmc.ncbi.nlm.nih.gov/articles/PMC2843567/)), the normal PDW range is approximately **9–17 fL**. The current values (150–520 fL) are off by an order of magnitude.

Additionally, as noted in the issue, neither LabCorp nor Quest include PDW in their standard CBC panels, but correcting the range is the minimal fix that preserves backward compatibility for users who rely on the PDW observation in their synthetic data.

## Solution

Corrected the PDW range from `{"low": 150, "high": 520}` to `{"low": 9, "high": 17}` in all 9 module JSON files where LOINC 32207-3 observations are defined:

### Files Changed
- `src/main/resources/modules/anemia/anemia_sub.json` — 4 PDW observations
- `src/main/resources/modules/bone_marrow_transplant.json` — 2 PDW observations
- `src/main/resources/modules/colorectal_cancer.json` — 1 PDW observation
- `src/main/resources/modules/hiv/hiv_baseline.json` — 2 PDW observations
- `src/main/resources/modules/kidney_transplant.json` — 2 PDW observations
- `src/main/resources/modules/lung_cancer.json` — 2 PDW observations
- `src/main/resources/modules/uti/ed_bundle.json` — 2 PDW observations
- `src/main/resources/modules/veteran_prostate_cancer.json` — 1 PDW observation
- `src/main/resources/modules/wellness_encounters.json` — 1 PDW observation

## Verification

- All 9 modified JSON files pass `json.load()` validation
- The adjacent Platelet Count (LOINC 777-3, range 150–450 ×10³/µL) and MPV (LOINC 32623-1, range 9.4–12.4 fL) ranges are unchanged and remain correct
- No other LOINC codes were modified

## Changelog

| Date | Change | Author |
|------|--------|--------|
| 2026-06-18 | Correct PDW range from 150-520 to 9-17 fL in 9 module files | rtmalikian |

### Files Changed
- `src/main/resources/modules/anemia/anemia_sub.json` — PDW range 150-520 → 9-17 fL
- `src/main/resources/modules/bone_marrow_transplant.json` — PDW range 150-520 → 9-17 fL
- `src/main/resources/modules/colorectal_cancer.json` — PDW range 150-520 → 9-17 fL
- `src/main/resources/modules/hiv/hiv_baseline.json` — PDW range 150-520 → 9-17 fL
- `src/main/resources/modules/kidney_transplant.json` — PDW range 150-520 → 9-17 fL
- `src/main/resources/modules/lung_cancer.json` — PDW range 150-520 → 9-17 fL
- `src/main/resources/modules/uti/ed_bundle.json` — PDW range 150-520 → 9-17 fL
- `src/main/resources/modules/veteran_prostate_cancer.json` — PDW range 150-520 → 9-17 fL
- `src/main/resources/modules/wellness_encounters.json` — PDW range 150-520 → 9-17 fL

### Verification
- All 9 modified JSON files validated with `json.load()`
- Only PDW ranges (LOINC 32207-3) were modified; adjacent lab values unchanged
- Reference: [PMC2843567](https://pmc.ncbi.nlm.nih.gov/articles/PMC2843567/) — typical PDW values ~17 fL

---

**About the Author:** Raphael Malikian — Clinical AI Solutions Architect. I specialise in building and fixing AI/ML systems for healthcare, including vector databases, RAG pipelines, and clinical NLP. If you need help with your project or think I can add value to your organisation, feel free to reach out — I'd love to connect.

📧 rtmalikian@gmail.com
🔗 GitHub: https://github.com/rtmalikian
🔗 LinkedIn: http://www.linkedin.com/in/raphael-t-malikian-mbbs-bsc-hons-71075436a

---

**Disclosure:** This code was developed with assistance from **mimo-v2.5-pro** (Xiaomi) via **Hermes Agent** (Nous Research). All changes were reviewed, tested against the actual codebase, and verified for correctness.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d02dcd65b0c8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.