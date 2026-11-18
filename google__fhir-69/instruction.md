# Issue

**Title:** Add Strongly Typed Resource Accessors to FhirPackage & Manager

## Description

Add Strongly Typed Resource Accessors to FhirPackage & Manager

- Make FhirPackage and FhirPackageManager generics over the types of the
  resources they contain.
- Add type-safe accessors get_structure_definition, get_search_parameter,
  get_code_system and get_value_set which retrieve resources of the requested
  type and maintain type safety over get_resource which has a return type of
  generic Message.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bf52d44c8bcc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.