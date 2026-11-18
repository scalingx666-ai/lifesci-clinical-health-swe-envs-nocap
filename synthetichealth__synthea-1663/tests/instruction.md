# Issue

**Title:** Use exact decimal for employer premium share

## Description

## Summary
- Replace `new BigDecimal(double)` with `BigDecimal.valueOf(double)` for employer premium share calculations
- Preserve clean decimal scale for premium expenses instead of introducing binary floating-point artifacts
- Add a regression assertion for employer-covered premium formatting

.

## Testing
- `./gradlew test --tests org.mitre.synthea.world.agents.PayerTest.employerPremiumCoverage`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c48eac705e15`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.