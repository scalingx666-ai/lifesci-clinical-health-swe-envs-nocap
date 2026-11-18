# Issue

**Title:** Configuration option to disable pretty printing for XML and JSON

## Description

The following exporters will now use the `exporter.pretty_print` configuration setting:

- FHIR (all versions)
  - Pretty printing settings are ignored when using `exporter.fhir.bulk_data` 
- CCDA
- JSON

The savings in C-CDA file size is low, only around 2% smaller.
The savings in FHIR file size can be quite large, approximately 33% smaller in most cases.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5ca9cb95c539`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.