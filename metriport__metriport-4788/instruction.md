# Issue

**Title:** ENG-1109: better formatting of notes

## Description

Issues:

- https://linear.app/metriport/issue/ENG-1109
- https://linear.app/metriport/issue/ENG-1111

### Dependencies

- none

### Description

- preserve spacing and new lines inside the text for better formatting on Frontend
- Run test converter same as `develop-fhir-resource-count.json`

<img width="894" height="865" alt="Screenshot 2025-10-01 at 11 40 41 AM" src="https://github.com/user-attachments/assets/04aceb4c-b2bf-4fc6-bf06-131859273f37" />

### Testing

- Local
  - [x] fhir converter run successfully
  - [x] UI tests 
  - [x] ⚠️ FHIR integration test suite 
    - include screenshots for proof
- Staging
  - none
- Sandbox
  - none
- Production
  - none

### Release Plan

- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Bug Fixes**
  * Preserve original line breaks and spacing in converted CDA text and embedded base64 content to improve readability and match source formatting.
  * Prevent unwanted trimming and collapsing of whitespace so text concatenations retain intended spacing.

* **Chores**
  * Updated integration test and helper scripts to use the new test paths and added safer extraction/error handling for test outputs.

* **Documentation**
  * Extended usage and monitoring notes for the integration test.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1fc222d5ed28`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.