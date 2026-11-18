# Issue

**Title:** fix(buying): book the exchange difference rows with matching account currency amounts

## Description

**Problem:** for a Purchase Receipt made from a foreign currency Purchase Invoice at another exchange rate, the two exchange difference rows pass the company currency amount on one side and a negative account currency amount on the debit side (`credit=d, debit_in_account_currency=-d`). `toggle_debit_credit_if_negative` then moves the negative debit to the credit side, so Stock Received But Not Billed gets twice the difference in account currency and Exchange Gain/Loss gets it on the opposite side.

**Fix:** drop the explicit account currency amounts so `get_gl_dict` sets them from the company currency amounts, and round the exchange difference to the field precision.

### Steps to reproduce
1. INR company with perpetual inventory, USD supplier.
2. Purchase Invoice without Update Stock: USD, exchange rate 85, 10 @ 10.
3. Create → Purchase Receipt, change the exchange rate to 83 and submit.
4. Compare Debit / Credit with Debit / Credit in Account Currency on the receipt's GL Entries.

Before: Stock Received But Not Billed Cr 8,500 / Cr 8,700 in account currency, Exchange Gain/Loss Dr 200 / Cr 200. After: the account currency amounts equal the company currency amounts.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6c8576d9754e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.