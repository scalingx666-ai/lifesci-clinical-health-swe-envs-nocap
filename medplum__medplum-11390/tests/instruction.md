# Issue

**Title:** fix(server): omit Authorization from bot event.headers

## Description

CDS Hooks, Bot $execute and bot-implemented custom operations passed the raw request headers to bots, including the caller's Authorization header. Bots already receive an access token for their runAs membership, so the caller's Authorization header is now removed from event.headers. Other request headers, including Cookie, are unchanged.

Anonymous /webhook routes are unchanged, since webhook senders authenticate to the bot with their own Authorization header.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cd70174b821a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.