# Issue

**Title:** TRUNK-6820: Write the DWR document type when creating dwr-modules.xml

## Description

## Description of what I changed

`WebModuleUtil` tags each module's entries in `dwr-modules.xml` with a `moduleId` attribute so they can be removed when the module stops, and DWR validates the file against a DTD that did not declare it, so every startup with legacyui logged:

```
ERROR - CommonsLoggingOutput.error(75) | Line=4 Attribute "moduleId" must be declared for element type "allow".
ERROR - CommonsLoggingOutput.error(75) | Line=384 Attribute "moduleId" must be declared for element type "signatures".
```

That is fixed in the DTD itself, which legacyui's DWR resolves from openmrs-contrib-dwr:  declares `moduleId` and lets the file hold the entries of any number of modules. The second part also clears `The content of element type "dwr" must match "(init?,allow?,signatures?)"`, which a second module with dwr config (htmlformentry, atlas, appointmentscheduling, reportingcompatibility) triggers and which an internal subset in this file could not fix.

What remains in core: `createDwrModulesXml`, which `startModule` and `stopModule` use when the file is missing, wrote no document type at all, so DWR had no grammar to validate the file against, and `Listener` kept the file that way on every restart. It now writes the same document type `Listener` writes.

## Verification

- `WebModuleUtilTest.createDwrModulesXml_shouldDeclareTheDwrDocumentType` fails on master and passes here. `mvn test -pl api,web`: api 5515 tests, web 200 tests, 0 failures.
- `jetty:run` with 31 modules and legacyui carrying the openmrs-contrib-dwr#7 jar: no DWR validation errors on startup (master with the current jar logs the two above), and `/openmrs/dwr/interface/DWRPatientService.js` still serves all 10 functions.

## Issue I worked on

see https://openmrs.atlassian.net/browse/TRUNK-6820

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01FBB3ZQetWQqkHrZQk9US1C

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b9993c839cf8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.