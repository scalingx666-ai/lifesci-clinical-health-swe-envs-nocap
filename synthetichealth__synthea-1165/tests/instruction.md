# Issue

**Title:** FIPS County (CSV Exporter) and SSA County (RIF Exporter)

## Description

- Update CSV exporter to include patient FIPS county code and more frequently populate the zip code.
   - Addresses #1124 
- Fixes SSA County code default value (the default was `22090`)  to try county name matching or picking a county within the correct state.
   - Before this fix, approximately 200+ county codes would be the default in 10,000.
   - With just county name looked up, usage of the default code drops from ~200+ to ~30 in 10,000.
   - The last ~30 or so now default to a random county in the correct state.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `afb9f156f7ce`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.