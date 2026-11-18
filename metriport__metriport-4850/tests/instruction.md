# Issue

**Title:** PATCH RELEASE Adjust FHIR Converter Service ECS config

## Description

Part of ENG-000

### Description

- 1 CPU = 1 worker thread
- 4x the number of ECS tasks
- Based on this discussion - [Slack link](https://metriport.slack.com/archives/C04DMKE9DME/p1760025846441979?thread_ts=1760024783.165279&cid=C04DMKE9DME)

### Testing
- N/A

### Release Plan

- :warning: Points to `master`
- [ ] Merge this
- Monitor performance

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

- Chores
  - Optimized production infrastructure to increase horizontal task capacity while reducing per-task CPU, improving scalability, throughput, and responsiveness during peak traffic. Memory and timeouts remain unchanged.
  - No changes to non-production environments.
  - End-user impact: faster handling of concurrent requests and improved reliability under load; no changes to UI or workflows.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c9148e85aad6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.