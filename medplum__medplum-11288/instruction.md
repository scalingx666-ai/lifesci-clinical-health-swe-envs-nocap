# Issue

**Title:** [Scheduling] Match service facilities anywhere in the name

## Description

Add an optional `searchParam` prop to MultiResourceInput and ResourceInput that overrides the search parameter/modifier that the input from the component is sent through.

In the case of these "Service facility" fields, we use `name:contains` instead of the default `name` search, which moves from a prefix-match to a case-insensitive search across the entire string.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dcf975363df0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.