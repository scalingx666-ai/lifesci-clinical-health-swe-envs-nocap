# Issue

**Title:** OBPIH-7894 Added specs reproducing review findings for Excel export

## Description

Specs for the review findings on #6179. See findings in attached PDF [PR #6179 Findings vs Tests.pdf](https://github.com/user-attachments/files/33508127/PR.6179.Findings.vs.Tests.pdf)

The ones covering bugs and regressions fail on purpose and should pass once each is fixed:

- Column indexes sort as strings (AA before B, "10" before "2") and the sort mutates the config's own field list
- ExcelWriterConfig.validate() skips BulkDataWriterConfigValidator
- The field's custom formatter is ignored for Number values
- ConfiguresExcelWriter advertises XLSX but no writer supports it
- Binder field types are read from the export DTO instead of the import DTO, and inherited fields throw NoSuchFieldException
- ExcelReaderConfig sheetName default of "Sheet1" hides the "multiple sheets" error

Marked @PendingFeature assuming we might not fix these immediately, but open to these being included / enabled in our test suite.
- XLSX writing (needs the POI upgrade?)
- number precision beyond what a double holds (needs a decision)
- and the CsvWriterConfig.validate() MissingMethodException that already exists on develop (separate ticket).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `36df9006c19b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.