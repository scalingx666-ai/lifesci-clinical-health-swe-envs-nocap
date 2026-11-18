# Issue

**Title:** fix(manufacturing): use the Blanket Order exchange rate for a price list in the order currency (backport #67490)

## Description

On a Blanket Order whose price list is in the order currency (not the company currency), changing the Exchange Rate kept the old Price List Exchange Rate, so the price list rate was converted between two rates of the same currency: 100 USD became 97.65 USD after 83 → 85.

Fix: when the price list currency is the order currency, use the order's Exchange Rate as the Price List Exchange Rate, as other transactions do.

Steps to reproduce:
1. Company in INR. Selling Price List in USD with an Item Price of 100 for FG.
2. Selling Blanket Order in USD with this price list, FG qty 10. Exchange Rate and Price List Exchange Rate are 83, Rate 100.
3. Change the Exchange Rate to 85.
4. Before: Price List Rate and Rate 97.65 USD. After: 100 USD, Price List Exchange Rate 85.

<hr>This is an automatic backport of pull request #67490 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b3cbafb9db0c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.