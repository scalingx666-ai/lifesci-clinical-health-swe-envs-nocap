# Issue

**Title:** Fill the secondary payer columns in claims.csv only for secondary payers

## Description

`CSVExporter.exportClaim` fills `STATUS2`, `OUTSTANDING2`, `LASTBILLEDDATE2` and `HEALTHCARECLAIMTYPEID2` when the claim's secondary payer is the no insurance payer, and leaves them empty when there is a real secondary payer. Each of those columns is guarded by

```java
if (claim.getSecondaryPayer() != null
    && claim.getSecondaryPayer().isNoInsurance()) {
```

The negation was lost in 9dd82c11, when `claim.secondaryPayer != Payer.noInsurance` was rewritten as `isNoInsurance()`. So every claim without secondary coverage reports a CLOSED/BILLED status, an outstanding balance, a billed date and a claim type for a payer it doesn't have, and claims that do have a `SECONDARYPATIENTINSURANCEID` get those columns empty with a claim type of 0. In a 5-patient run aged 70-90 (seed 1717), all 466 claims without secondary insurance had `STATUS2=CLOSED`, and none of the 185 claims with a secondary payer had a `STATUS2`.

### Changes

- `exportClaim` now works out once whether the claim has a secondary payer. It uses the same check (`!isNoInsurance()`) that `SECONDARYPATIENTINSURANCEID` already uses, and every payer 2 column reads that value. With no secondary payer the columns are empty and `HEALTHCARECLAIMTYPEID2` is `0`, as before. With a secondary payer they are filled in the same way the payer 1 columns are.
- The `SECONDARYPATIENTINSURANCEID` check now reads the secondary payer from the claim being written (`claim`) and not from `encounter.claim`. The ID it writes already came from `claim`, so the check and the value now come from the same claim. For encounter claims the two are the same object.
- I left the existing `TODO` about the `OUTSTANDING2` amount in the BILLED branch alone.

### Testing

New `CSVExporterClaimsTest.testClaimSecondaryPayerColumns` generates 10 patients aged 70-90, so plenty of their claims carry Medicare supplemental coverage. It then checks every row of `claims.csv`. Rows without `SECONDARYPATIENTINSURANCEID` must have empty payer 2 columns and `HEALTHCARECLAIMTYPEID2=0`. Rows with it must have `STATUS2` equal to `STATUS1`, non-empty `OUTSTANDING2` and `LASTBILLEDDATE2`, and `HEALTHCARECLAIMTYPEID2` equal to `HEALTHCARECLAIMTYPEID1`. The test fails on master (`expected:<[]> but was:<[CLOSED]>`) and passes with this change.

- `./gradlew test --tests 'org.mitre.synthea.export.*'`: 144 tests, 0 failures, 2 skipped
- `./gradlew checkstyleMain checkstyleTest`: no new warnings

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d9d07a6eef91`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.