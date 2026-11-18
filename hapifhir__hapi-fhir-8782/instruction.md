# Issue

**Title:** 8779 write only patch is applied but returns 403 forbidden

## Description

## Problem
Since #8254, a client with write but no read access to a resource gets `403` on `PATCH`, even though the patch has already been committed. The response is read-authorized after the DAO transaction finishes.

## Fix
When the caller can't read the patched resource, return `200` with no body (as with `Prefer: return=minimal`) instead of failing a committed write. The #8253 protection still holds: the resource isn't disclosed.

`AuthorizationInterceptor`:
- `hookPreShow` skips `PATCH`. The response body is read-authorized only in `hookOutgoingResponse`.
- New `@Hook(SERVER_OUTGOING_RESPONSE) hookOutgoingResponse(RequestDetails, IBaseResource, ResponseDetails, Pointcut)` clears the response resource for a PATCH the caller can't read. For other responses, it calls the old 3-arg method.
- The old 3-arg `hookOutgoingResponse` is kept, `@Deprecated` and no longer a `@Hook`. Routing through it keeps existing subclass overrides working.

## Tests
- `AuthorizationInterceptorWriteResponseJpaR4Test`: write-only PATCH now expects `200` with an empty body, and the patch is stored. Also adds a `Prefer: return=representation` case. A plain read is still `403`.
- `AuthorizationInterceptorR4Test`: a subclass override of the deprecated method still runs.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `48e175c73fdd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.