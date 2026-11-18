# Issue

**Title:** Imaging Integration Block vote tickets from 11 Nov 2026

## Description

## HL7 FHIR Pull Request

_Note: No pull requests will be accepted against `./source` unless logged in the_ [HL7 Jira issue tracker](https://jira.hl7.org/projects/FHIR/issues/).

If you made changes to any files within `./source` please indicate the Jira tracker number this pull request is associated with: `   `

## Description

* ImagingStudy and ImagingSelection
    * FHIR-57946 * Update endpoint text to include current DICOM service names
* ImagingStudy
    * FHIR-58169 / FHIR-59573 * Correct ist-4 and ist-5
    * FHIR-59627
      * Fix event mapping exceptions
* ImagingSelection
	* FHIR-57945 / FHIR-57950
	  * Update ISL-1 to support DocumentReference payload
	  * Add DocumentReference example
	* FHIR-57943
	  * Clarified relationship between `studyUid` and `derivedFrom` when it references an Imaging Study
	* FHIR-57944
	  * Identified that some subset elements can have more than one DICOM source

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9e5ba0b6ef72`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.