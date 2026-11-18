# Issue

**Title:** J#58533 Adding a search parameter to the newly added ResearchStudy.acronym element

## Description

The Jira ticket doesn't specify that a search parameter is needed for the new ResearchStudy.acronym element, but it'd be useful: https://jira.hl7.org/browse/FHIR-58533

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `97f905eb5698`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.