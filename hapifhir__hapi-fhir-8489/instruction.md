# Issue

**Title:** 8487 Fix _has with chained reference when token system is a URL with path segments

## Description

In a `_has` search with a chained reference parameter, e.g. `Organization?_has:Task:owner:patient.identifier=http://example.com/id/foo/123|21`, `QueryStack.createPredicateHas` parsed the value without passing the chain (`.identifier`) as the qualifier. `ReferenceParam` therefore treated the value as an absolute reference URL with resource type `foo`, and the search failed with `HAPI-1250: Invalid/unsupported resource type`. Values without slashes (e.g. `21` or `urn:system|21`) happened to work.

When the parameter inside `_has` is a reference with a chain, the chain is now passed as the qualifier, so the value is parsed the same way as in a regular chained search (`Task?patient.identifier=...`). Other parameter types and the nested `_has` / `_id` cases are unchanged.

Added `FhirResourceDaoR4SearchNoFtTest#testHasParameterChained_tokenValueWithUrlSystem`, which covers `system|value`, value only, and no match.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e67398597537`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.