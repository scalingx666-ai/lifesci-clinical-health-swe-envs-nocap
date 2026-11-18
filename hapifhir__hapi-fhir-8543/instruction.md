# Issue

**Title:** 8523 state code validation error with extensible binding

## Description

## Problem
Some values have no code system of their own, like a state code in `Address.state`. When a profile binds one of these to a ValueSet whose codes all come from a single code system, HAPI assumes the value belongs to that code system and checks it there too. If the value isn't in the ValueSet (for example `ON` against a list of US state codes), that extra check reported an error, even though the binding is extensible and should only give a warning. As a result, valid resources such as Locations with Canadian addresses were rejected.

## Fix
When HAPI has assumed the code system and the value isn't in the ValueSet, the extra check is skipped. Only the usual "not in the value set" message is reported, and its severity follows the binding strength, so an extensible binding gives a warning. Values that name their code system are still checked against it. tx.fhir.org and Ontoserver behave the same way.

## Tests
- New tests in `WorkerContextValidationSupportAdapterTest` and `FhirResourceDaoR4ValidateTest`.
- 8 existing validator tests expected the extra error message alongside the binding error. They now expect the binding error only.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c0def8fa3ca6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.