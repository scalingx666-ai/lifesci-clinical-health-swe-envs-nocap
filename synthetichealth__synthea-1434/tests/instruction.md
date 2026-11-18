# Issue

**Title:** Add support for code system versions

## Description

Addresses #1430

For the most part, the SNOMED codes we use come from the International edition, but there are a few that are US-specific. This causes errors when validating generated resources that use these code, because if the resource doesn't specify the version, the validator/tx server will assume the international edition.

This PR adds a `version` field to our HealthRecord.code model which allows the version to be specified, and updates the codes that currently cause errors. The new version field is optional since it's only really relevant to half a dozen codes. See corresponding PR on the module builder: 

Codes that were changed:
5251000175109 -- the one from the linked issue, added US version flag
784051000000106 -- Depression care management, replaced with an international code that already had the same display
449411000124106 -- Admission to SNF, added US version
449381000124108 -- Discharge from SNF, added US version
457551000124104 -- Acute cerebrovascular accident (disorder), this code is inactive so I replaced it with international Cerebrovascular accident
452331000124102 -- Review of imaging finding, added US version
454711000124102 -- Depression screening PHQ2, added US version
231181000000100 -- delivery of spinal cord injury rehab is UK specific, I just deleted the activity. Not sure it adds anything over the code on the CarePlan

For reference, list of SNOMED edition URIs: https://confluence.ihtsdotools.org/display/DOCEXTPG/4.4.2+Edition+URI+Examples

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6fa1b4b11084`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.