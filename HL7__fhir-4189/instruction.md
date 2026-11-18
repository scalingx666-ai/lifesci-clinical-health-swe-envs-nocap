# Issue

**Title:** FHIR-56264: Address DeviceAlert "currency"

## Description

## HL7 FHIR Pull Request

_Note: No pull requests will be accepted against `./source` unless logged in the_ [HL7 Jira issue tracker](https://jira.hl7.org/projects/FHIR/issues/).

If you made changes to any files within `./source` please indicate the Jira tracker number this pull request is associated with: `FHIR-56264`

## Description

* removed `DeviceAlert.presence`, and made `occurrence` into type Period (rather than dateTime or Period), updated search parameters to align
* added new signal identifier element and search parameter
* renamed `indication` to `period`
* updated Background and Context section with, hopefully, a clearer diagram and with new text

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb54341c7b4e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.