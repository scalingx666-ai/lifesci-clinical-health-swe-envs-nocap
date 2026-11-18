# Issue

**Title:** add a bamboo specific scramble and unscramble method

## Description

Part of ENG-1122

_[Release PRs:]_

Issues:

- https://linear.app/metriport/issue/ENG-1122

### Dependencies
None

### Description
Add bamboo specific scramble and unscramble for identifier.
"+ to a dash, and an = to a period" <-What the code should do
### Testing
- Local
  - [x] Send a Bamboo msg over to mllp server using new scramble method


  - [x] Upload to local SFTP server as if Bamboo to make sure all identifiers dont have + or =
  
<img width="396" height="45" alt="Screenshot 2025-09-24 at 6 58 49 PM" src="https://github.com/user-attachments/assets/1f6eb72b-5125-43e3-9965-3ff5828903f9" />

- Staging
Cant test VPC Peering stack isnt deployed + Bamboo config doesnt exist

- Production
Can't test



<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

- New Features
  - Automatic translation of Bamboo-formatted patient IDs for inbound messages; reflected in logging, webhooks, acknowledgements, and roster generation.
  - Roster generation now conditionally transforms rows for Bamboo HIEs to enforce Bamboo ID formatting.
  - Early HIE detection applied to message processing.

- Bug Fixes
  - Improved validation and error handling for missing patient IDs.
  - More consistent roster sizing after transformations.

- Tests
  - Unit tests updated for new ID handling and configuration behavior.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `040bd5974e4b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.