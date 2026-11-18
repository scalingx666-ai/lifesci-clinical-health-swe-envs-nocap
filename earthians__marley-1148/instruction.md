# Issue

**Title:** fix: skip sample collection creation for return sales invoices

## Description

Issue Description:-
When Create Observation on Sales Invoice Submission is enabled in Healthcare Settings, submitting a Sales Invoice with billable observation-template items automatically creates downstream diagnostic records such as Sample Collection and related observation flow.

The same submit logic was also running for return Sales Invoices / credit notes. Because of that, when a user created a credit note for a refunded or cancelled lab test, the system incorrectly created a new Sample Collection workflow again with that credit note no as reference.

This is incorrect because a return invoice is meant to reverse billing, not initiate a fresh sample collection process.

Fix Applied:-
Updated the Sales Invoice submit logic in utils.py to skip sample collection / observation creation for return invoices.
                 Applied a return guard before calling:
                           create_sample_collection_and_observation(doc)
                 Guard condition:
                        not doc.get("is_return")
                      not doc.get("return_against")

Result:
- normal Sales Invoices continue to create sample collection/observation flow as before
- return Sales Invoices / credit notes no longer create new Sample Collection records from this submit path

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ce8da2514f84`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.