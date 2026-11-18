# Issue

**Title:** fix(sample-collection): set status to Pending when no samples are collected

## Description

Issue Description:-
When a Sample Collection document is created and none of its child samples have been collected yet, the parent document status was showing Partly Collected instead of Pending.

Expected behavior:
        - if no samples are collected: Pending
        - if some samples are collected: Partly Collected
        - if all samples are collected: Collected

Actual behavior:

- if at least one child row was not Collected, the parent status logic defaulted to Partly Collected
- this incorrectly included the “nothing collected yet” case
- This also caused confusion in related flows like creating observations from service requests, because the document lifecycle no longer matched the allowed/expected status sequence.

Fix Applied:-
Updated the status calculation in sample_collection.py in two places:
      validate()
      update_collection_status()

The logic is now:

- Collected if all child rows are Collected
- Pending if all child rows are Open
- Partly Collected otherwise


Flow After Fix:-

- A Sample Collection document is created.
- If every sample row is still Open, parent status remains Pending.
- When one or more sample rows become collected while others are still open, parent status becomes Partly Collected.
- When every sample row becomes Collected, parent status becomes Collected.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `55b1143f36c3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.