# Issue

**Title:** Fix ids for flexporter executeScript

## Description

# Summary
Fixes an issue with the flexporter where mappings that use `execute_script` export files without ids on the resources.

## New behavior
Resets ids by searching for and removing `urn:uuid:`. Now flexporter run appropriately exports resources with ids when executing a script during mapping.

## Code changes
Copies code from [line 151 of RunFlexporter.java](https://github.com/synthetichealth/synthea/blob/055d977ec40f52cd5d386395297930241ad4e34c/src/main/java/RunFlexporter.java#L151) which is used to fix an issue with HAPI ids. (Thanks for the fix @dehall!)

# Testing guidance
Run the synthea flexporter with something like `./run_synthea -fm {mapping_file.yaml}` where the mapping file contains some `execute_script` mapping as described in the [flexporter wiki](https://github.com/synthetichealth/synthea/wiki/Flexporter#execute-script). Look at the output patient file in output/fhir and confirm that the appropriate resources are exported with id fields.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `055d977ec40f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.