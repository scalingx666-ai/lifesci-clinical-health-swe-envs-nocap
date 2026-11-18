# Issue

**Title:** 8232 cds hook prefetch template resolution doesnt resolve values from resolved prefetch

## Description

Bug issue :  
 
 - `%prefetchKey.fhirpath` expressions in prefetch templates never resolved because CdsPrefetchSvc was calling the context of substituteTemplate, which had no access to the request's prefetch map.
  - Changed `findMissingPrefetch()` to use LinkedHashSet (preserving declaration order), ensuring a prefetch entry that depends on an earlier entry is always resolved after it.
  - Wrapped ClassCastException in handleFhirPathPart with a descriptive InvalidRequestException; changed resolveAsIdOnlyStub to log-and-return-null on unknown resource types instead of throwing (the FhirPath engine swallows exceptions from resolveReference callbacks, making the throw unreachable).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fd1806f291ff`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.