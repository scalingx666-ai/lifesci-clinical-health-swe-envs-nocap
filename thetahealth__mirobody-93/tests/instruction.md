# Issue

**Title:** data: code health-store batches as devices

## Description

## Device sourced records through `/api/data`

A record that identifies a supported health store now uses the shipped device crosswalk. Known vendor fields reach their catalogue metric and LOINC code; an ambiguous or unknown identifier is kept as sent. Other records retain manual provenance.

Updated against the 1.5.2 main branch. Mixed source requests now pass one provenance per row into **one observation transaction**, so a later failure cannot commit an earlier source group on its own. The response still includes `rejected` counts.

Verified locally: a mixed Health Connect/manual batch calls ingest once and codes to 8867-4/718-7; 41 observation tests pass; Ruff, compileall and six import contracts pass. Current GitHub checks are shown in the PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d6aaf2efe056`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.