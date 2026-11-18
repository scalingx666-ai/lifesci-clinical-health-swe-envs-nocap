# Issue

**Title:** Pharmacy: FHIR-58591, 55007, 53089, 59365, 59309, 53978, 54095, 53977, 55888

## Description

Pharmacy WG ticket batch. One commit per ticket, plus one commit for the MedicationStatement mapping exceptions regenerated for FHIR-55888. Supersedes #4325, which closed when its branch was renamed to `jct-pharm`.

| Ticket | Disposition | Change |
|---|---|---|
| [FHIR-58591](https://jira.hl7.org/browse/FHIR-58591) | Persuasive | Typo "Insruction" fixed in the MedicationRequest Dispenser Instruction Codes value set description |
| [FHIR-55007](https://jira.hl7.org/browse/FHIR-55007) | Persuasive with Mod | `MedicationRequest.device` now `CodeableReference(DeviceDefinition \| Device)`; comment: Device is primarily for instance orders |
| [FHIR-53089](https://jira.hl7.org/browse/FHIR-53089) | Persuasive with Mod | Removed the unused code system `http://hl7.org/fhir/reason-medication-not-given`; the `statusReason` example binding still uses the SNOMED CT value set; OID kept in `oids.ini` |
| [FHIR-59365](https://jira.hl7.org/browse/FHIR-59365) | Persuasive with Mod | `dosage.html`: three lowercase modal words changed to MAY/SHOULD/MAY; the "Balloters should" sentence is unchanged |
| [FHIR-59309](https://jira.hl7.org/browse/FHIR-59309) | Persuasive with Mod | `MedicationRequest.informationSource` now allows Device; short/definition say "person, organization, or device"; comment gives an AI-system example |
| [FHIR-53978](https://jira.hl7.org/browse/FHIR-53978) | Persuasive | MedicationRequest scope typos ("can can", "medications ... NOT to be taken", DeviceRequest link) |
| [FHIR-54095](https://jira.hl7.org/browse/FHIR-54095) | Persuasive | "Device Request" to DeviceRequest (text fixed in the FHIR-53978 commit; this commit adds the release note) |
| [FHIR-53977](https://jira.hl7.org/browse/FHIR-53977) | Persuasive | MedicationStatement grammar ("should be recorded", "resulting in", "record medications") |
| [FHIR-55888](https://jira.hl7.org/browse/FHIR-55888) | Persuasive with Mod | Restored `MedicationStatement.basedOn` as in R4 (0..* Reference(MedicationRequest \| CarePlan \| ServiceRequest)); comments on `basedOn` and `derivedFrom` explain how they differ; no search parameter added |

Each changed resource has a ticket entry under "Changes since 6.0.0-ballot5" in its introduction (MedicationRequest, MedicationAdministration, MedicationStatement). `dosage.html` has none (datatype page, non-substantive change).

**Changes made by the build**
- `medicationstatement-event-mapping-exceptions.xml` regenerated for the new `basedOn` element (`fd14cbe72f`).
- Build-regenerated files that are not part of these tickets (Procedure and Questionnaire mapping exceptions, `source/spelling/add.txt`, `tools/tx/snomed/snomed.xml`) are not included: they were restored to master in a separate commit.

**Validation**
- Full build `./gradlew publishFull` (`-nopartial`): exit 0, `Summary: Errors=0, Warnings=3771, Information messages=571`. No baseline build of master was run, so there is no warning delta; no warning mentions the changed elements.
- Partial build `./gradlew publish`: exit 0, `Errors=0, Warnings=114`.
- I checked each ticket in the generated pages (`publish/`), and every ticket passed. In the full build's regenerated `valuesets.json`, `reason-medication-not-given-codes` appears only as the ValueSet; the CodeSystem is gone (FHIR-53089).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `68b299928d75`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.