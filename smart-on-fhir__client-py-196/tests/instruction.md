# Issue

**Title:** Add PKCE parameters to authorization code exchange

## Description

I've added a test, but it doesn't really verify that the challenge is computed properly, since it's the same code in both the test and the code. I have tested this with my medplum testing environment, and verified that injecting a typo in the verifier does result in rejected authorization, as it should.

Should be fully backward compatible even with servers that don't support PKCE, because authorization servers [are required to ignore unsupported parameters](https://datatracker.ietf.org/doc/html/rfc6749#:~:text=The%20authorization%20server%20MUST%20ignore).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ba579be42b8b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.