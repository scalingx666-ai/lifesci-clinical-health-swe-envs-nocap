# Issue

**Title:** fix(server): resolve the Agent of an agent connection in the token's own project

## Description

The agent WebSocket connect and transmit handlers now read the Agent in the access token's own Project, consistent with linked Projects being read-only. A connection only reports status for its agent once the Agent has been resolved. Agent operations such as `$push` and `$status` are unchanged.

## Changes
- `ws/agent.ts`: add `readAgentInOwnProject()` and use it in the connect and transmit handlers. Super admins are unaffected.
- `ws/agent.test.ts`: tests for agent connections with linked Projects.

## Compatibility
Agents that connect with credentials from the Agent's own Project are unaffected. An agent whose credentials belong to a different Project than its `Agent` resource should use credentials from the Agent's own Project.

## Testing
- `npx vitest run src/ws/agent.test.ts src/fhir/operations/agent src/fhir/operations/utils/agent`: 106 passed

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `35f70cf8e436`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.