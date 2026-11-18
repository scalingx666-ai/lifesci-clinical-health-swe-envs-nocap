# Issue

**Title:** OBPIH-7995 root cause not deserializing in Cycle Count

## Description

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:** https://pihemr.atlassian.net/browse/OBPIH-7995

**Description:** This is because the structure of how enums are represented in JSON has changed with the new object mapper.

new format:

```
"discrepancyReasonCode": "DAMAGED",
```
old format:

```
"discrepancyReasonCode": {
    "enumType": "org.pih.warehouse.core.ReasonCode",
    "name": "DAMAGED"
},
```
I fixed the frontend to account for this. This only impacts APIs that use the new BaseController, which currently is just CC and receiving

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `04d8e3d3dea6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.