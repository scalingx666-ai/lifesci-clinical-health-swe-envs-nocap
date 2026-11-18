# Issue

**Title:** Export every payer transition referenced by exported claim transactions

## Description

## What was broken

`claims_transactions.PATIENTINSURANCEID` is documented as a foreign key to `payer_transitions.MEMBERID`, and since #1602 it holds the member id of the claim's plan record. Some of those ids have no row in `payer_transitions.csv`: in the official sample data every unresolved id belongs to a claim dated before 1970, and the earliest `payer_transitions.START_DATE` in that file is 1969-02-22.

## Root cause

`CSVExporter.export(Person, long)` called `exportPayerTransitions(person, 0L, time)`. The `0L` was meant as "no lower bound" but it is the Unix epoch, so `exportPayerTransitions` only kept plans with `getStopTime() >= 1970-01-01`. Plans that ended before 1970 were never written, while the claims made under them were (when `exporter.years_of_history` keeps the full history), so the member ids in `PATIENTINSURANCEID` had nothing to join to.

## What changed

- `exportPayerTransitions` no longer takes a lower bound. It writes every plan that started on or before the end of the simulation, so the plan behind every exported claim transaction is present in `payer_transitions.csv`. The column set of both files is unchanged.
- New test `CSVExporterTest.testClaimTransactionsReferenceExportedPayerTransitions` generates a seeded population aged 60-90 with `exporter.years_of_history = 0`, checks that the export contains claim transactions dated before 1970, and asserts that every non-empty `PATIENTINSURANCEID` matches a `(PATIENT, MEMBERID)` pair in `payer_transitions.csv`. It fails on `master` (hundreds of unresolved rows, all dated 1968) and passes with this change.

## Testing

```
./gradlew test --tests '*CSVExporterTest*'
# 12 tests, 0 failures (new test fails before the fix, passes after)

./gradlew checkstyleMain checkstyleTest
# no violations in the changed files (one pre-existing LineLength warning in src/main/java/App.java:47)
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d9d07a6eef91`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.