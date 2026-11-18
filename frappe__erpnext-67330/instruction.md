# Issue

**Title:** fix(manufacturing): cost BOM rows at the Item Price valid today

## Description

With Rate of Materials based on Price List, the BOM looked up the Item Price without a date. So it took the price with the latest Valid From, even a future one, and also used expired prices.

Fix: pass today as the transaction date, so only the Item Price valid today is used.

Steps to reproduce:
1. Create a buying Price List. For item RM add an Item Price of 10 valid from 30 days ago and one of 12 valid from 30 days ahead. For item RM2 add 7, valid from 60 days ago to 30 days ago.
2. Create a BOM with Rate of Materials based on Price List, that Price List, and rows RM qty 1 and RM2 qty 1. Save.
3. RM is costed at 12 and RM2 at 7. They should be 10 and 0 ("Price not found").

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3e08476bb7b3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.