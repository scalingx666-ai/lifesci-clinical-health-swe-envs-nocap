# Issue

**Title:** Fix converter parser compatibility with ANTLR 4.13.1

## Description

## Summary
Fix converter initialization failures when a consuming application loads
ANTLR runtime 4.13.1. The existing ANTLR 4.8-generated parser calls the
unavailable ATNDeserializer.Deserialize(char[]) method.

- Update Antlr4.Runtime.Standard to 4.13.1.
- Align the combined NuGet package's ANTLR dependency floor.
- Regenerate six checked-in C# parsing files using ANTLR 4.13.1.
- Preserve the existing grammar, conversion templates, and test source.
- Align the combined package's Ensure.That dependency floor to 10.1.0,
  matching the existing project references, as suggested in review.

## Validation
- Converter unit tests: 406 passed, 0 failed.
- Representative functional conversions: 191 passed, 0 failed,
  covering HL7v2, CCDA, STU3-to-R4, and JSON.
- Confirmed resolved ANTLR runtime version 4.13.1.
- Existing build/test warnings were not suppressed.
- Ensure.That metadata follow-up: Release build and local-only package
  inspection confirmed Ensure.That 10.1.0 and ANTLR 4.13.1 dependency floors.

## Release considerations
Publish a new package version through the normal release process;
no package has been published by this change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `70fd328e0501`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.