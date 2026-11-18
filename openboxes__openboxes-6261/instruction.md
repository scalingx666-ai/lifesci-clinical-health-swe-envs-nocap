# Issue

**Title:** OBLS-1003 Fix three timing-dependent regression specs

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:**
https://openboxes.atlassian.net/browse/OBLS-1003 ()

**Description:**

Three regression specs from #6252 failed intermittently on CI runs of #6258 and #6262. Each depended on timing; this
makes them deterministic. Test-only; no application code changes.

## Inventory baselines in `ServiceIntegrationSpec.stock()`

`ProductAvailabilityServiceIntegrationSpec` > "the bin locations of a depot as of a date" expected 8 and got 3.

- `stock()` recorded each lot as its own inventory baseline. A baseline (`PRODUCT_INVENTORY`) is a product-wide
  count: in `InventoryService.getQuantityByProductAndInventoryItemMap` the latest one replaces every earlier count
  of the product.
- Two baselines of one product were still both counted when they compared equal (`Transaction.compareTo`: same
  transaction date and same `dateCreated`, to the second) - Groovy's `!=` on `Comparable` uses `compareTo`. When
  the two saves fell into different seconds, only the last lot counted.
- `stock()` now puts the lots of a product stocked as baselines (any `PRODUCT_INVENTORY` type) at the same date
  (the default date is one value per feature) into one transaction, as a real count does. Calls with other
  transaction types or other dates are unchanged.

The same setup was used by `StockMovementServiceOutboundIntegrationSpec`, `DashboardServiceIntegrationSpec` and the
product merge feature of `ProductAvailabilityServiceIntegrationSpec`.

## Pending, then completed receipt in `ShippingContractSpec`

"POST /partialReceiving/{id} PENDING then the echoed COMPLETED body receives the shipment" got a 400:
`transactionDate` rejected.

- The pending receipt is delivered "now". MySQL stores it to the second and rounds, so it can be up to half a
  second in the future; the completed receipt's transaction takes that date, and `Transaction` refuses a date after
  now.
- The spec now waits until the stored delivery date has passed before sending the completed body (at most about
  half a second). The bodies stay the ones the app sends. (`PartialReceivingApiSpec` already avoids this by sending a
  delivery date a minute in the past.)

## Background job runs in the OBAF specs

`AutoReceiptIntegrationSpec` > "a fully received shipment is not received again; a pending receipt blocks the
automatic one" failed with an optimistic locking exception on the shipment.

- `BootStrap` starts the Quartz scheduler in integration tests too. Shipping to an `AUTO_RECEIVING` depot publishes
  `AutomaticReceiptEvent`, and `AutomaticReceiptEventService` schedules `AutomaticReceiptJob` a second later (the same
  for `AutomaticBackorderReallocationJob`). That run received the shipment while the feature was receiving it.
- `ObafIntegrationSpec` already pauses the cron triggers. It now also installs, once per test JVM, a trigger listener
  that vetoes every run of these two jobs not fired by `QuartzRunner` (the features that test the jobs fire them
  through it). Quartz asks the listener on the worker thread just before the job runs, so a run already queued is
  stopped too.

## Verification (local, JDK 8, Testcontainers)

- Forced the timing:
  - with a 1.1 s pause between the two lots in the availability spec's setup, the old `stock()` fails 2 of its 3
    features (the one seen in CI and "product availability is refreshed for a whole depot ...", which had the same
    latent problem); with this change all 3 pass;
  - with a 1.5 s pause after shipping in `AutoReceiptIntegrationSpec`, the old setup fails 2 of its 8 features (the
    background run receives the shipment first); with this change all 8 pass.
- The specs that use the changed setup: 41 tests (`stock()` and `ShippingContractSpec`) and 269 tests (all OBAF
  specs), 0 failed.
- Full `regressionIntegrationTest` on MySQL 8.0.36 and on MariaDB 10.3.39: 1245 tests, 0 failed, 272 skipped each.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f815bac6fb89`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.