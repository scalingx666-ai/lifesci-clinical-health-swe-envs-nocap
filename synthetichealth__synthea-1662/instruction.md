# Issue

**Title:** Avoid max timestamp in CCDA coverage fallback

## Description

## Summary
- Stop CCDA export from adding a fallback no-insurance coverage record at `Long.MAX_VALUE`
- Keep the existing fallback coverage at export time so CCDA export can continue when no current plan exists
- Add a regression test that verifies CCDA export does not leave a payer history entry ending at `Long.MAX_VALUE`

.

## Testing
- `./gradlew test --tests org.mitre.synthea.export.CCDAExporterTest`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c48eac705e15`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.