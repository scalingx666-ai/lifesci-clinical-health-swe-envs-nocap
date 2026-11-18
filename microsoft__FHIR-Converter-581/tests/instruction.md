# Issue

**Title:** Better handling of a template data mismatch error case

## Description

In this PR I handle a case where a template calls a Filter that expects hl7 data but what was passed in was fhir. So, in this case there is no hl7 passed in and it fails with a generic message (ie Internal server error with 500) in the convert. This change is needed so that in convert we can catch this specific case and respond with a better message.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `88a84ed71ece`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.