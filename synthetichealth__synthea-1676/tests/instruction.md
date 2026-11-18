# Issue

**Title:** fix: set Claim.total to sum of item.net values in FHIR exports

## Description

## Problem

FHIR `Claim.total` does not equal the sum of `Claim.item.net` values, violating the [FHIR R4 specification](https://hl7.org/fhir/R4/claim-definitions.html#Claim.total) which states:

> *"Total amount of the claim. The Claim.total represents the sum of the item.net values for all claim items."*

Two root causes:

1. **Missing net value on encounter item**: Item 1 (the encounter itself) was added to the Claim resource without a `net` value, even though the encounter cost was included in `Claim.total`.

2. **Post-adjustment vs pre-adjustment mismatch**: `Claim.total` was set to `getTotalClaimCost()` (the post-insurance-adjustment amount), while `item.net` values used raw pre-adjustment costs from `entry.getCost()`. This created cases where the total was significantly different from the sum of items (e.g., total $704.20 vs item sum $1,968.84).

## Solution

- Added the encounter cost as a `net` value on item 1 in both `FhirR4.java` and `FhirStu3.java`
- Track the running sum of all `item.net` values as items are added
- Use the accumulated sum for `Claim.total` instead of `getTotalClaimCost()`

This guarantees `Claim.total = Σ(Claim.item.net)` as required by the FHIR specification.

## Verification

- `./gradlew compileJava` — BUILD SUCCESSFUL
- `./gradlew test --tests "*Claim*"` — BUILD SUCCESSFUL
- `./gradlew test --tests "*FhirR4*"` — BUILD SUCCESSFUL

## Files Changed

- `src/main/java/org/mitre/synthea/export/FhirR4.java` — encounter item net + total calculation
- `src/main/java/org/mitre/synthea/export/FhirStu3.java` — same fix for STU3 exporter

---

**About the Author:** Raphael Malikian — Clinical AI Solutions Architect. I specialise in building and fixing AI/ML systems for healthcare, including vector databases, RAG pipelines, and clinical NLP. If you need help with your project or think I can add value to your organisation, feel free to reach out — I'd love to connect.

📧 rtmalikian@gmail.com
🔗 GitHub: https://github.com/rtmalikian
🔗 LinkedIn: http://www.linkedin.com/in/raphael-t-malikian-mbbs-bsc-hons-71075436a

---

**Disclosure:** This code was developed with assistance from **mimo-2.5-pro** (Xiaomi) via **Hermes Agent** (Nous Research). All changes were reviewed, tested against the actual codebase, and verified for correctness.

## Changelog

| Date | Change | Author |
|------|--------|--------|
| 2026-06-18 | Initial fix: set Claim.total to sum of item.net values | rtmalikian |
| 2026-06-18 | Added DCO sign-off to commit | rtmalikian |
| 2026-06-18 | Updated PR documentation with changelog | rtmalikian |

### Files Changed
- `src/main/java/org/mitre/synthea/export/FhirR4.java` — Compute Claim.total as sum of item.net values for FHIR R4 exports
- `src/main/java/org/mitre/synthea/export/FhirStu3.java` — Applied same fix for STU3 exports

### Verification
- ✅ FHIR Claim.total now equals sum of Claim.item.net values
- ✅ Complies with FHIR R4 specification requirement
- ✅ DCO sign-off present on all commits

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d02dcd65b0c8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.