# Issue

**Title:** Fix queries using the platform for query plugins that implements QueryInterface

## Description

Fix the problem of queries using the platform for query plugins that implements QueryInterface. This will avoid the plugin of query to implement QueryDimInterface, if it is not expected to. 

An example of the issue was: 

```
Task<Iterable<SearchResult>> result = this.platform.query("lucene", "*:*", extraFields);
result.get();
```

It was reported by @rlebre.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `65eafc91ebc1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.