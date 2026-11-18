# Issue

**Title:** fix(backend): redeem invitation codes and rotate refresh tokens atomically

## Description

Invitation codes and refresh tokens are meant to be used once, but the validity check and the "mark as used" write were separate steps. Requests that arrived at the same time could all pass the check, and each one got its own tokens. With this change, the check and the write are one database operation, so only one of several concurrent requests succeeds.

## Changes

- **Invitation code redemption.** Only one of several concurrent redeems of the same code gets tokens. The others get the usual "Invalid or expired invitation code" response.
- **Refresh token rotation.** Only one of several concurrent refreshes with the same refresh token gets a new token pair. The others get the usual 401. This applies to both SDK and developer tokens. Revoking a refresh token works the same way.
- **No burned credentials on failure.** The code or old token is marked as used in the same transaction that stores the new refresh token. If issuing the new tokens fails, the code or old token can still be used.

## Verification

I ran the backend locally and sent 20 simultaneous requests with the same credential through the public API. The table shows how many of the 20 got new tokens:

| Scenario | Before | After (6 runs) |
|---|---|---|
| Redeem one invitation code | 1, 3, 5, 1, 9, 17 (6 runs) | 1 every time, the rest 404 |
| Refresh one SDK refresh token | 9 | 1 every time, the rest 401 |
| Refresh one developer refresh token | 4 | 1 every time, the rest 401 |

Before the fix, one invitation code produced up to 17 separate sessions for the same user. After the fix, the server logs show no errors or deadlocks.

## Behavior change

A client that sends two refresh requests at the same time with the same refresh token now always gets a 401 on one of them. Before, both could succeed by chance. Clients should send one refresh at a time and use the newest refresh token.

When the same user is deleted at the moment they redeem a code or refresh a token, the database can detect a deadlock and abort one of the two operations. This needs both to happen within milliseconds of each other, and retrying succeeds.


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

## Bug Fixes

* Invitation codes and refresh tokens can no longer be successfully redeemed or refreshed by multiple simultaneous requests.
* If issuing replacement tokens fails, the original refresh token remains usable, and an invitation code can be retried.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `74a817da085f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.