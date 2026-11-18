# Issue

**Title:** Evaluate each OR'ed date or quantity alternative with its own prefix

## Description

## Problem

An OR list on a `date` or `quantity` parameter whose alternatives use different prefixes returns wrong results. For example `Observation?date=lt2020-01-01,gt2022-01-01` is evaluated as if both alternatives were `lt`, and `Observation?value-quantity=lt5,gt10` likewise.

## Root cause

`QueryStack.searchForIdsWithAndOr` (DATE and QUANTITY cases) derives a single `CompareOperation` from the first element of the OR group and passes it to `createPredicateDate` / `createPredicateQuantity`. That operation then overrides the prefix of every other alternative. The same happens through conventional chains (`Observation?subject.birthdate=...`): they go back through `ResourceLinkPredicateBuilder` to `searchForIdsWithAndOr`, so they were affected. `createIndexPredicate` is the embedded/uplifted path and normally receives a null operation. In `createPredicateDate` the operation was applied to every alternative in the loop (`QueryStack.java` ~line 975); in `createPredicateQuantity` likewise (~line 1458).

## Fix

Inside the per-alternative loops of `createPredicateDate` (~line 975-981) and `createPredicateQuantity` (~line 1458-1462), the operation is derived from that alternative's own prefix with `toOperation(prefix)`; an alternative without a prefix is `eq`, so `value-quantity=gt15,10` means `>15 OR =10`. For a date alternative that is not a `DateParam` the operation passed in is still used.

`_filter` passes a single-element list and carries its operator in `theOperation`. The date branch already encoded the operator as the `DateParam` prefix (`fromOperation`). The quantity branch (~line 1141-1150) did not, so it now does the same (`QuantityParam.setPrefix(fromOperation(op))`). Operators with no prefix equivalent (`co`, `sw`, `ew`, ...) cannot be turned into a prefix; `fromOperation`/`toOperation` would silently map them to `eq`. To keep the previous behaviour, the per-alternative loops only derive the operation from the prefix when the incoming operation is null or has a prefix equivalent (`QueryParameterUtils.hasPrefixEquivalent`); otherwise it is passed on unchanged and rejected as before (date: `HAPI-1255 Unsupported operator specified`; quantity: `HAPI-1235 Unable to handle quantity prefix`), both `InvalidRequestException`.

## Tests

Only R4 non-fulltext tests were exercised (module `hapi-fhir-jpaserver-test-r4`, JPA H2).

`FhirResourceDaoR4SearchNoFtTest`:
- `testDateSearchOrWithDifferentPrefixes` (12 cases, including unprefixed alternatives mixed with prefixed ones)
- `testQuantitySearchOrWithDifferentPrefixes` (15 cases; `5|10` and `gt5|10` are controls that also pass without the fix, `gt15|ne10` and `ne10|gt15` discriminate)
- `testChainedDateSearchOrWithDifferentPrefixes` (4 cases through `Observation?subject.birthdate=...`)

`FhirResourceDaoR4FilterTest` (regression controls, all pass on the parent commit too):
- `testFilterQuantityAndDateOperators` (11 cases): `_filter` with `eq/ne/gt/ge/lt/le` on `value-quantity` and `date`
- `testFilterUnsupportedOperatorOnDateAndQuantity` (6 cases): `co/sw/ew` on `date` and `value-quantity` are still rejected

Classes run in full: `FhirResourceDaoR4SearchNoFtTest`, `FhirResourceDaoR4FilterTest`, `FhirResourceDaoR4SearchCustomSearchParamTest` : SearchNoFtTest 192 (1 skipped), FilterTest 57, SearchCustomSearchParamTest 48 (2 skipped); 297 total, 0 failures.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0338ffd19fb7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.