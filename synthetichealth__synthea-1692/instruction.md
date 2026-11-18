# Issue

**Title:** Honor the configured code system when adding FHIR code translations

## Description

`FhirR4.addTranslation` took a code system, used it to look up a `CodeMapper`, and then always emitted the ICD-10-CM system URI. It also only ever asked for the ICD-10-CM mapper, so a map registered under any other `exporter.code_map.<system>` key was loaded at startup and never consulted, even though `Exporter#loadCodeMappers` documents that usage and gives CPT as its example.

Apply every configured code map and label each translation with its own system URI. Output for the shipped ICD-10-CM configuration is unchanged.

Also add the CPT system URI, match system names case-insensitively so that names derived from configuration keys resolve, and hold the code mappers in a `TreeMap` so that multiple maps are applied in a deterministic order.

Adds some fun and exciting tests!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7e08387c68a7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.