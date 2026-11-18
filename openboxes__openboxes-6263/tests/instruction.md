# Issue

**Title:** Calculate quantity on hand in the database

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:** #6201

**Description:**

This is the first part of the fix for #6201, where the transaction report can run the server out of memory.

The report gets its opening and closing balances from `getAvailableItemsAtDateAsMap`. For a past date, that loads every transaction entry of the products at the facility into memory and replays them, and the report does it twice per request. For a busy facility that's tens of thousands of Hibernate entities per request.

This PR calculates those balances in the database instead:

- **`getQuantityOnHandAtDate`** (new) does the same calculation as a single SQL aggregate and only loads the inventory items and bins that have stock.
- **`getQuantityOnHandAtDateAsMap`** (new) is the report's entry point. For the current date it still reads `product_availability`, the same as before.
- **Only the transaction report uses it** (the summary and the single-product dialog). Every other caller of `getAvailableItemsAtDate` keeps the existing in-memory replay: product inventory transactions (cycle counts and record stock), inventory import, migrations and `LoadDataService`.

#### Calculation rules

The query follows the same rules as the replay in `InventoryService.getQuantityByProductAndInventoryItemMap`:

1. Transactions are ordered by transaction date, then by date created.
2. The most recent `PRODUCT_INVENTORY` transaction (product inventory or inventory baseline) resets every inventory item of the product.
3. The most recent `INVENTORY` transaction resets a single inventory item.
4. `DEBIT` quantities are subtracted, everything else is added.

Two edge cases are handled explicitly and documented in the Javadoc:

- **Ties.** Transaction dates are stored to the second, and a baseline and its adjustment are often saved together. When a credit or debit has exactly the same transaction date and date created as a baseline, it's applied after the baseline. If two baselines tie, the one with the highest id wins.
- **A product count followed by lot counts.** If every entry of a `PRODUCT_INVENTORY` has a later `INVENTORY` transaction, the replay skips the product inventory, but this query still resets the whole product. `INVENTORY` transactions are legacy data (#165), so this only affects old history.

#### Other changes

- **The Adjustments column is renamed to Net Change.** The value is the closing balance minus the opening balance, so it already includes credits and debits. It isn't a total of the adjustment transactions, and the old name suggested it was.
- **MariaDB:** the query runs with `split_materialized=off`, using `SET STATEMENT` so it only applies to this query. Without it, MariaDB turns the baseline subqueries into lateral derived tables that are re-executed for every transaction entry, which takes the query from seconds to many minutes. MySQL doesn't have this optimization, so the query runs unchanged there.

#### Tests

`ProductAvailabilityServiceQuantityOnHandAtDateSpec` (15 tests):

- covers each rule and both edge cases above
- checks that `getAvailableItemsAtDate` still uses the in-memory replay
- compares the result against the replay for 200 random transactions

All tests pass on MySQL 8.0.36 and MariaDB 10.3.39.

#### Not in this PR

This removes the balance calculation from memory, but the report still loads the transactions inside the date range as full entities and groups them with an O(n²) loop. Those are the next part of #6201.

#### How to test

1. Run the transaction report for a facility with a lot of history and a date range in the past. Compare the Opening, Closing and Net Change values with `develop`. They should match, except in the two edge cases above.
2. Open the single-product dialog for a few rows. The opening and closing balances should match the summary row.
3. Run a cycle count or record stock and confirm the adjustments are calculated as before. That code path is unchanged.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01RqDhKQyrN4ZX1iZUg4RvAm

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a19378538056`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.