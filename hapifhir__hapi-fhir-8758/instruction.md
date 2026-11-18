# Issue

**Title:** Server level interceptors are not invoked during processing of $meta-add/$meta-delete operations

## Description

## Problem

`BaseHapiFhirResourceDao.doMetaAdd` and `doMetaDelete` fired `STORAGE_PRESTORAGE_RESOURCE_UPDATED` and
`STORAGE_PRECOMMIT_RESOURCE_UPDATED` on the storage level only. Interceptors registered at the server level capable of influencing the operation outcome like the `AuthorizationInterceptor` are not invoked.

## Change

- `doMetaAdd` and `doMetaDelete` now call `doCallHooks(...)` for both pointcuts, the same as the update path
  (`BaseHapiFhirDao.notifyInterceptors`).
- Changelog: `9_0_0/8751-meta-add-meta-delete-call-restfulserver-interceptors.yaml`.

## Tests

New tests in `ResourceProviderInterceptorR4Test` register interceptors on the `RestfulServer`:

- `testMetaAdd_callsRestfulServerStorageHooks_addTags` and `testMetaDelete_callsRestfulServerStorageHooks_deleteTags`
  check that both hooks are called with the old and new resource, and that the stored resource has the change.
- `testMetaAdd_restfulServerPreStorageHookRejects_tagIsNotStored` and
  `testMetaDelete_restfulServerPreStorageHookRejects_tagIsNotRemoved` check that a `RestfulServer`
  interceptor that throws at `STORAGE_PRESTORAGE_RESOURCE_UPDATED` blocks the change.

Partially generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d13a8f38ae73`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.