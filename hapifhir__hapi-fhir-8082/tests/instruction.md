# Issue

**Title:** GL-8878: Pre-fetch bare-form conditional-create ifNoneExist URLs

## Description

## Summary

This PR fixes a gap in `TransactionProcessor.preFetchConditionalUrls` where conditional-create entries using the FHIR-spec bare query form of `ifNoneExist` (e.g. `identifier=http://system|value`, with no leading `?`) were excluded from the batched pre-fetch pass and instead fell through to per-entry match searches at write time. The full-URL form (`Patient?identifier=http://system|value`) was already batched correctly; this change canonicalizes the bare form to the full form before the same pre-fetch path, so `STORAGE_PRESEARCH_REGISTERED` consumers see identical hook flow for both.

1. `canonicalizeIfNoneExistUrl` is extracted as a private static helper that normalizes all three variants (bare, full, degenerate `?`-leading) into `[ResourceType]?[params]` form.
2. The `POST`/`ifNoneExist` branch in `preFetchConditionalUrls` drops the `contains("?")` guard and routes all non-blank `ifNoneExist` values through canonicalization before calling `processConditionalUrlForPreFetching`.
3. A new `FhirSystemDaoR4Test` test (`testTransactionMultipleBareConditionalCreates_ArePreFetchedLikeFullForm`) verifies that a 5-entry bundle of bare-form conditional creates issues no more SELECT queries than the equivalent full-form bundle, and that no duplicate resources are created.

Companion to Smile CDR MR https://gitlab.com/simpatico.ai/cdr/-/merge_requests/7280

## Code Review Suggestions

- [ ] `canonicalizeIfNoneExistUrl`: the degenerate `?query` case (`questionMarkIndex == 0`) prepends `theResourceType` without a `?` — verify this produces `Patient?query` not `Patientquery` (it does: the leading `?` is still present in `theIfNoneExist`).
- [ ] The `isNotBlank` guard replaces `contains("?")` — confirm no callers can reach `processConditionalUrlForPreFetching` with a blank string that would previously have been excluded by the old guard.
- [ ] The test uses `myCaptureQueriesListener.countSelectQueries()` as a proxy for "batched vs. N+1"; confirm the test environment actually registers `CaptureQueriesListener` so the count is non-zero and meaningful.
- [ ] The absolute `isLessThan(entryCount)` assertion catches the case where both paths regress equally — verify the threshold is tight enough (5 entries, any 1 batch query) to be useful without being brittle.

## QA Test Suggestions

### Setup
- [ ] Deploy a CDR instance with tokenization enabled on `Patient.identifier` (identifier normalization) and at least one HL7v2 ingestion channel active.

### Test Cases
- [ ] Submit a FHIR transaction bundle containing multiple bare-form conditional-create entries (e.g. from an HL7v2 ADT feed) and confirm: (a) resources are created on first submission, (b) repeated submission is idempotent (no duplicates), and (c) no HAPI-0929/HAPI-0539 errors appear in the CDR log.
- [ ] Submit the same bundle using full-form `ifNoneExist` URLs and confirm identical behaviour and identical DB query counts (confirm via CDR metrics or DB slow-query log).
- [ ] Confirm that a single-entry REST conditional create via `If-None-Exist` header (bare form, spec-compliant external client) still resolves correctly.
- [ ] Confirm that existing full-form conditional-create bundles are unaffected by the change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `510a505c6f49`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.