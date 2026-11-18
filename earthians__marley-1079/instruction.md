# Issue

**Title:** fix: pass frappe._dict to get_item_price in treatment counselling (backport #1078)

## Description

- get_item_price accesses its first argument via dot notation (pctx.price_list), but args was a plain dict. Changed it to frappe._dict to support attribute access.<hr>This is an automatic backport of pull request #1078 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5ce84b9895a6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.