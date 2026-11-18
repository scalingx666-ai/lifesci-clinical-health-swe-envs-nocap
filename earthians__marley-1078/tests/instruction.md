# Issue

**Title:** fix: pass frappe._dict to get_item_price in treatment counselling

## Description

- get_item_price accesses its first argument via dot notation (pctx.price_list), but args was a plain dict. Changed it to frappe._dict to support attribute access.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0f42451029cb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.