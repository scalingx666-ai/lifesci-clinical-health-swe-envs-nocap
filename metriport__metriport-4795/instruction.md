# Issue

**Title:** build: custom ai summary and pdf tweak

## Description

Part of cs-2472

Issues:

- https://linear.app/metriport/issue/CS-2472
- https://linear.app/metriport/issue/CS-2473

### Dependencies

- Upstream: none
- Downstream: none

### Description

- Add a new AI Summary prompt for recent visits 
- Update the MR Summary to include isChronic and HCC codes in the Conditions table

### Testing

- Local
  - [x] The AI summary generates the expected output
  - [x] The Conditions table contains the isChronic and HCC codes
- Staging
  - [x] The AI summary generates the expected output
  - [x] The Conditions table contains the isChronic and HCC codes
- Sandbox
  - [ ] The AI summary generates the expected output
  - [ ] The Conditions table contains the isChronic and HCC codes
- Production
  - [ ] The AI summary generates the expected output
  - [ ] The Conditions table contains the isChronic and HCC codes


### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

- **New Features**
  - Introduced “Recent Visit” AI summary with per-customer feature-flag support; recent-visit summaries are prioritized when enabled.
  - New structured prompts for recent-visit and unified date handling for PCP/recent summaries.
  - AI summarization dynamically selects a 1–2 year timeframe based on available data for fuller results.
  - Conditions table now includes a Chronic column and displays HCC codes.

- **Bug Fixes**
  - Fixed medication filtering to exclude inactive/unknown statuses.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `97dc6bf50c18`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.