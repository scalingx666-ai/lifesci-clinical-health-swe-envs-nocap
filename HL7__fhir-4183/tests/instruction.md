# Issue

**Title:** FHIR-53723: Container additional information

## Description

Resolves [FHIR-53723](https://jira.hl7.org/browse/FHIR-53723): Container additional information

## What changed
Aligned additive and container/device modeling across the Specimen, SpecimenDefinition, Device, and DeviceDefinition resources. Specimen.processing.additive was changed from a CodeableReference into a backbone element with type (CodeableReference(SubstanceDefinition|Substance)) and quantity (SimpleQuantity), and Specimen.collection/processing/container.device were narrowed from a CodeableConcept|Reference(Device)|canonical(DeviceDefinition) choice to CodeableReference(Device) bound to the containerdevice-code value set. In SpecimenDefinition, the typeTested.container material/type/cap/description/capacity elements were collapsed into a single device[x] choice (CodeableConcept bound to containerdevice-code, or canonical(DeviceDefinition)), and the container.additive backbone was restructured to type (CodeableReference(SubstanceDefinition)) plus quantity. Device.additive.type gained a Substance target alongside SubstanceDefinition, and a matching additive backbone (type + quantity) was added to DeviceDefinition. The three Specimen device token search parameters were repointed to .device.concept, the SpecimenDefinition container search parameter was repointed to the new device[x], and the affected Specimen/SpecimenDefinition examples were updated to the new structures. Full Gradle publish completed with 0 errors.

## Files touched
- `source/device/structuredefinition-Device.xml`
- `source/devicedefinition/structuredefinition-DeviceDefinition.xml`
- `source/specimen/bundle-Specimen-search-params.xml`
- `source/specimen/specimen-example-liver-biopsy.xml`
- `source/specimen/specimen-example-urine.xml`
- `source/specimen/specimen-example.xml`
- `source/specimen/structuredefinition-Specimen.xml`
- `source/specimendefinition/bundle-SpecimenDefinition-search-params.xml`
- `source/specimendefinition/specimen-example-serum-plasma.xml`
- `source/specimendefinition/specimendefinition-example-serum-plasma.xml`
- `source/specimendefinition/specimendefinition-example.xml`
- `source/specimendefinition/structuredefinition-SpecimenDefinition.xml`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `15863a9b2ca0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.