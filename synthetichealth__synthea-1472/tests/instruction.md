# Issue

**Title:** Remove SHR extensions from FHIR exporters

## Description

The SHR extensions are at best out of date, and at worst are potentially pointing people towards malware ( #1471 ). This just removes them. 

Unfortunately we also used the SHR extension for the passport Identifier in the Patient resource, so I replaced that with the hl7 recommended system (see the list at https://terminology.hl7.org/identifiers.html ) but made it configurable since we know people want to run synthea for other countries.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e6534b629952`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.