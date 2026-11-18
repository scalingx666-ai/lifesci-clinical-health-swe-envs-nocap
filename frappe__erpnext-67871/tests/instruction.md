# Issue

**Title:** test: stop fetching live exchange rates in four tests (backport #67775)

## Description

Four tests asked the live exchange-rate provider for a rate that no test data stored. When the provider did not answer (as on 2026-11-17 around 07:20 UTC), the rate came back as 0 and these tests failed in unrelated merge-queue batches on develop and version-16-hotfix:

- `TestQuotation.test_make_quotation_qar_to_inr`: "Exchange Rate is mandatory"
- `TestSalesInvoice.test_rounding_adjustment_in_foreign_currency`: `ZeroDivisionError` in `get_payment_entry`
- `TestSubscription.test_multi_currency_subscription` and `test_multi_currency_subscription_with_default_company_currency`: "Exchange Rate is mandatory"

The JPY test and the 2018 USD subscription tests now store the rate they need as a Currency Exchange record. QAR is pegged to USD but INR is not, so a stored record never applies there and the rate always comes from the provider. That test now patches `requests.get` with the existing provider stub from `test_currency_exchange` and checks the pegged conversion against the stubbed USD to INR rate.

### Steps to reproduce

1. Block outgoing access to `api.frankfurter.dev`.
2. Run `bench --site <site> run-tests --module erpnext.selling.doctype.quotation.test_quotation --test test_make_quotation_qar_to_inr`.
3. It fails with "Exchange Rate is mandatory". With this change it passes.
<hr>This is an automatic backport of pull request #67775 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `acb0ba0054b1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.