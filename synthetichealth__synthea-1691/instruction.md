# Issue

**Title:** Add NPI columns to organizations.csv and providers.csv

## Description

Synthea assigns every organization and clinician an NPI with a valid CMS check digit, but the CSV exporter writes only internal UUIDs. Clinician NPIs reach the FHIR Practitioner resource, organization NPIs reach no exporter at all, and neither reaches CSV, so a consumer working from the CSV export cannot identify a provider by NPI.

Append an NPI column to both files. The column goes at the end of each row so that readers that index by position are unaffected.

Also correct the stale header comments on `exportOrganization` and `exportProvider,` which had not been updated when LAT and LON were added. This one is a bit of a drive-by, but seemed like a good fix to make while I was in the area :)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7e08387c68a7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.