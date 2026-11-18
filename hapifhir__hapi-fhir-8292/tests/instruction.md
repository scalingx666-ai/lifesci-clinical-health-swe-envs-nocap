# Issue

**Title:** Fix Upload Terminology intermittent test failures

## Description

**Root Cause**

The new terminology upload uses a `CodeSystem` staging mechanism which uses a placeholder `TermCodeSystemVersion` which is replaced with the actual `TermCodeSystemVersion` once all concepts and all related information to a CodeSystem are persisted. This adds records to the delete deferred queue which queues a delete job for the obsolete `TermCodeSystemVersion`. The terminology can also contain ValueSets which can trigger `ValueSet` async pre-expansion jobs. 

Upload terminology tests do not wait for the async processes to finish before doing the assertions. This results in intermittent test failures.

**Changes**

- `TerminologyTestHelper` successful imports now settle their own async work via a new private `awaitImportDeferredTerminologyWork()`: re-enable deferred processing, `saveAllDeferred()`, then await the version-delete, CodeSystem-delete, and pre-expansion jobs. Callers no longer need to know what an import leaves behind.                                                                                                                                       
                                                                                                                                                                                                              
- `TerminologySvcImplCurrentVersionR4Test` — fixed the self-comparing assertion in matchUnqualifiedIds and gave it the ID prefix as a parameter so both call sites assert against the right set.        

- replaced `validateExpandedTermConceptsForVersion` with `validateTermConcepts`, which keys concepts by `CodeSystem` version and asserts exactly one per version, so a leftover `DELETED_` version shows up as a readable map diff instead of an exception. Removed the `@AfterEach` job wait, dead helpers, and unused fields now that the helper handles the waiting.                                                                      
                                                                                                                                                                                                               
- updated the version-count assertions across the terminology upload tests e.g. `TerminologyLoaderSvcLoincJpaTest` such that each upload now leaves exactly one `TermCodeSystemVersion`. That is the correct final number once the replaced one is deleted, so counts drop from 2 per upload to 1. The reasoning is     captured once in `TermTestUtil.MSG_ONE_CODE_SYSTEM_VERSION_PER_UPLOAD` and used as the assertion message. 
- `TermCodeSystemDeleteJobTest.runDeleteJobMultipleVersions` now genuinely loads two versions instead of relying on the placeholder version to make up the count.     

**Note**

Another cause for intermittence was related to the scenario with multiple upload terminology operations executed sequentially. The tests relied on the fact that upload order is the same as persistence order for `TermCodeSystemVersion` records which is not necessarily the case. The queries in the test assertions were fixed already as part of #8274.
  
**Known issue**
  
Awaiting the pre-expansion jobs exposed a pre-existing production race condition in `TermDeferredStorageSvcImpl.saveAllDeferred`. `ValueSet` pre-expansion can start while the replaced `CodeSystem` version is still being deleted, and an expansion that runs in that window falls back to an unvalidated in-memory path. Filed as #8321. Worked included here is a second `saveAllDeferred()` call after the delete jobs complete, commented and linked to the issue.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `256f9fa3eecd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.