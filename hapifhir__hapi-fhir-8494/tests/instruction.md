# Issue

**Title:** Apply _lastUpdated range to the root HFJ_RESOURCE alias instead of a self-join

## Description

## Problem
Query: `ExplanationOfBenefit?created=ge2025-10-13&_lastUpdated=ge2026-07-28&_lastUpdated=le2026-10-13&_sort=_lastUpdated`

would generate SQL with a redundant join:
```sql
SELECT t1.RES_ID FROM HFJ_RESOURCE t1
INNER JOIN HFJ_SPIDX_DATE t0 ON (t1.RES_ID = t0.RES_ID)
INNER JOIN HFJ_RESOURCE t2 ON (t1.RES_ID = t2.RES_ID)
WHERE ((t0.HASH_IDENTITY = ?) AND (t0.SP_VALUE_HIGH_DATE_ORDINAL >= ?))
  AND ((t2.RES_UPDATED >= ?) AND (t2.RES_UPDATED <= ?))
ORDER BY t1.RES_UPDATED ASC
```

The redundant join only happens for a particular combination of search parameters. All three of these must be present:

1. at least one regular search parameter like `created` where its value is stored in an index table such as HFJ_SPIDX_DATE;
2. something that makes HFJ_RESOURCE the query root: a `_sort`, or a second regular search parameter;
3. a `_lastUpdated` parameter, with a lower bound, an upper bound, or both. Unlike regular search parameters, `_lastUpdated` has no index table. It is matched against the RES_UPDATED column of HFJ_RESOURCE itself, and its predicate must be placed on an HFJ_RESOURCE alias.

Each part of that search generates:

| Search part | Generated SQL |
|---|---|
| `_sort=_lastUpdated` | HFJ_RESOURCE becomes the query root: `FROM HFJ_RESOURCE t1`, with `ORDER BY t1.RES_UPDATED ASC` |
| `created=ge2025-10-13` | `INNER JOIN HFJ_SPIDX_DATE t0 ON (t1.RES_ID = t0.RES_ID)` with `(t0.HASH_IDENTITY = ?) AND (t0.SP_VALUE_HIGH_DATE_ORDINAL >= ?)` |
| `_lastUpdated=ge2026-07-28&_lastUpdated=le2026-10-13` | `INNER JOIN HFJ_RESOURCE t2 ON (t1.RES_ID = t2.RES_ID)` with `(t2.RES_UPDATED >= ?) AND (t2.RES_UPDATED <= ?)` |

The `_lastUpdated` part doesn't detect that the root `t1` is already HFJ_RESOURCE and joins a second copy, `t2`, on the primary key. The search result is correct, because `t2` is always the same row as `t1`, but it can be slow to execute on large databases:

- To return results in `_lastUpdated` order, the database reads the RES_UPDATED index on `t1` in order.
- The `_lastUpdated` range is only on `t2`.   As a result, the database can't use the index to start that read at the beginning of the range and starts from the oldest resource instead. For each row it looks up HFJ_SPIDX_DATE and only then applies the range on `t2`, continuing until it has enough matches.

## Fix
`SearchQueryBuilder.getOrCreateResourceTablePredicateBuilder()` now reuses the query root when it is already HFJ_RESOURCE, instead of adding a self-join.

## Tests
- Two new cases in `FhirResourceDaoR4SearchSqlTest.sqlGenerationTestCases()` (each run with and without partition joins): a `_lastUpdated` range with `_sort=_lastUpdated`, and a `_lastUpdated` range with two regular search parameters.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b644f54bbede`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.