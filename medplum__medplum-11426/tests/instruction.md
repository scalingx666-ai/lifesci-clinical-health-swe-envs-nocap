# Issue

**Title:** fix(server): set a login's membership only once under concurrent requests

## Description

`setLoginMembership()` checks that a Login has no membership yet, then saves the Login with the membership. Two requests for the same Login (for example two `POST /auth/profile` calls sent together) could both pass the check and both save, so the stored membership could differ from the one the first response was issued for.

## Changes

- `oauth/utils.ts`: the final save in `setLoginMembership()` uses `ifMatch` with the version of the Login that was checked, so only one concurrent request can set the membership. The other gets the existing "Login profile already set" error. This covers every caller: `/auth/profile`, `/auth/newproject`, `/auth/newpatient` and `tryLogin`.
- `auth/newpatient.ts`: `createPatient()` no longer writes the membership to the Login itself. `newPatientHandler` already sets it through `setLoginMembership()`, and the earlier write would now make that call fail.

## Compatibility

- When two requests race to set the membership of the same Login, the second now gets 400 "Login profile already set" instead of 200. Requests sent one after another behave as before.

## Testing

- `auth/profile.test.ts`: two concurrent `/auth/profile` requests for one Login; exactly one succeeds, and the stored membership is the one its code was issued for. Fails on `main`.
- Ran `src/auth`, `src/oauth` and `admin/project.test.ts`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e2ba31603169`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.