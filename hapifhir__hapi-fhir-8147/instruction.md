# Issue

**Title:** Patient-ID partition mode: transaction conditional update by identifier should not duplicate

## Description

.

In Patient-ID partition mode with an all-partition-search-capable backend, a transaction `PUT Patient?identifier=...` against an existing Patient either created a silent duplicate or failed with HAPI-1321, because the conditional match search was pinned to one write-derived partition instead of fanning out.

### Fixes

- **TransactionProcessor** — when all-partition search is supported, don't collapse an unresolvable conditional match search onto the outer write partition. Letting it fan out finds an existing Patient in another partition, so a mismatched body id now yields HAPI-2279 instead of a silent duplicate.
- **PatientIdPartitionInterceptor** — an id-less conditional PUT (`PUT Patient?identifier=X` with no body id) is rewritten after pre-fetch to a direct `PUT Patient/<id>` using the already-resolved match, so it updates the existing Patient instead of failing with HAPI-1321.
- **BaseTransactionProcessor.shouldConditionalUpdateMatchId** — no longer strips a *resolved* body id (placeholder ids still stripped), so a same-id conditional update stays routable and updates in place. See below.

### Why remove the resolved-id branch in `shouldConditionalUpdateMatchId`

This method decides whether to keep or strip the id carried on the resource **body** before a conditional update runs. The old code had a branch that stripped the body id whenever that id was already "resolved" during the transaction (checked via `TransactionDetails.hasResolvedResourceId`, keyed by the id's value). Once the TransactionProcessor fix above lets the conditional match search succeed, that branch breaks a **same-id** conditional update in Patient-ID partition mode. Consider `PUT Patient?identifier=X` whose body carries the existing Patient's own id `A`:

1. Pre-fetch resolves the identifier to the existing Patient `A` and registers `A` in the transaction's resolved-id set.
2. At write time, the branch checks the **body id** (`A`) against that set. Because `A` is now resolved, the check matches and the body id is **stripped** — the resource becomes id-less.
3. The write then determines the storage partition for that now id-less Patient. In Patient-ID partition mode the partition is `hash(id)`, which needs an id, so the request fails with **HAPI-1321** instead of updating Patient `A`.

Removing the branch keeps the matching body id, so the Patient stays routable and updates in place. Placeholder ids (`urn:` / `#`) are still stripped by the remaining check.

(The branch only ever affected the same-id case: it keys on the body id's own value, and only the matched id — not a *different* client-provided id — is in the resolved set. The different-body-id → HAPI-2279 behavior comes from the TransactionProcessor fix above, not from this branch.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e067fb720552`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.