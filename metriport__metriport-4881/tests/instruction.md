# Issue

**Title:** Add heartbeat monitors for adts

## Description

Part of ENG-000

### Dependencies

- Upstream: 

### Description
Add heartbeat monitors for:
- Konza
- Lahie
- Alohr
- Bamboo
- HealthConnectTexas
- HieTexacPCC

### Testing
- Staging
  - [x] Send a hl7 notification msg to the mllp server and see if the new Checkly monitor picks it up.
 <img width="1451" height="67" alt="Screenshot 2025-10-20 at 7 21 49 PM" src="https://github.com/user-attachments/assets/3f8d7a20-e193-43a4-907c-749d35a7620e" />

- Production
  - [ ] Look at new checkly monitors to make sure they are gettings pings.


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

## Release Notes

* **New Features**
  * Added heartbeat monitoring for HL7 notification webhooks to track service health and uptime.
  * System now supports optional monitoring endpoint configuration for Health Information Exchange connections.
  * Monitoring executes automatically alongside existing analytics and reporting processes.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5ad5ff16941b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.