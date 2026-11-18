# Issue

**Title:** Use interval for CCDA vital signs organizer

## Description

## Summary
- Export CCDA vital signs organizer `effectiveTime` as a low/high interval
- Use the earliest and latest vital sign observation timestamps for the interval bounds
- Add an XPath regression check that the vital signs organizer includes interval bounds

.

## Testing
- `./gradlew test --tests org.mitre.synthea.export.CCDAExporterTest`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c48eac705e15`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.