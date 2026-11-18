# Issue

**Title:** FHIRPath page batch 1

## Description

The following Jira tickets have been applied:
FHIR-54174 FHIR should refer to the latest version of the fhirpath specification
FHIR-53947 FHIRpath Intro section(s) general improvements
FHIR-54601 Handling of difference in range of FHIR.decimal and System.Decimal
FHIR-53811 Clarify hasValue() and getValue()
FHIR-53959 Additional Functions cleanup
FHIR-53950 Use of FHIR Quantity - clarification on units systems and internal representation
FHIR-53952 FHIR specific variables - clarifications and missing documentation on %profile
   (and a couple of minor spelling corrections)
FHIR-53962 `slice()` should this only be available in invariant definitions
FHIR-53951 all functions/features should have examples, return and argument types/cardinality should be explicit

These 2 have partially been applied: (still refining parts of the disposition - don't mark as completely applied)
FHIR-40271 FHIR is() example use non-singleton examples
FHIR-53948 Clarification in Using FHIR Types in Expressions

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a831fc08d9d6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.