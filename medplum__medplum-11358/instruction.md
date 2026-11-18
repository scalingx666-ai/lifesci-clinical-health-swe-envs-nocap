# Issue

**Title:** Linear-time dedupe in FHIRPath union and search token building

## Description

Saving a ValueSet with a large enumerated code list could use 100% CPU for minutes while holding an open database transaction. Postgres then killed the connection for sitting idle in the transaction for over 30 seconds, and the save failed. In production this left server tasks unresponsive until they exited.

The ValueSet `code` search parameter (`ValueSet.expansion.contains.code | ValueSet.compose.include.concept.code`) went through two duplicate-removal passes that compared every code against every code kept so far:
- `removeDuplicates`, which runs for every FHIRPath `|`, called `fhirPathEquals` for each pair.
- `convertToSearchableTokens` checked each new token with `result.some(...)`.

**Changes**
- `removeDuplicates`: strings and booleans are deduplicated with a `Set`. Under FHIRPath equality they only match the identical primitive. Numbers, quantities and objects still go through `fhirPathEquals`, but only against each other. Order and first occurrence are kept as before.
- `convertToSearchableTokens`: duplicates are tracked in a `Map<system, Set<value>>`, keyed on the lowercased value when `caseInsensitive` is on.
- `buildContactPointToken` no longer lowercases values itself. The server already passes `caseInsensitive` for ContactPoint parameters, and in-memory matching lowercases both sides.

**Behavior notes**
- With `caseInsensitive` on, values that differ only in case now produce one token instead of the same lowercase token twice. The stored token columns already deduplicated, so they don't change.
- `convertToSearchableTokens` is exported from `@medplum/core`. Called without `caseInsensitive`, it now returns ContactPoint values in their original case.

**Performance** (`buildResourceRow`, unique codes in `compose.include.concept`)

| Codes | Before | After |
|---|---|---|
| 20k | 3.3 s | 23 ms |
| 80k | 53.5 s | 97 ms |
| 160k | ~212 s (extrapolated) | 195 ms |

**Testing**
- Tests added for `removeDuplicates`: types aren't mixed up, nearly-equal numbers and deep-equal Codings are merged, the same value under different type tags is merged, and order is kept.
- Tests added for token dedupe: tokens are kept separate per system, and case variants merge when `caseInsensitive` is on.
- A one-off fuzz test compared the old and new `removeDuplicates` on 20,000 mixed-type arrays and found no differences.
- Core test suite passes, and the server's token, row-builder and search tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `619b001cd424`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.