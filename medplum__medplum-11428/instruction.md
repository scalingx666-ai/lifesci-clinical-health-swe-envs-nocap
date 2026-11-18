# Issue

**Title:** fix(server): give WebSocket binding tokens their own audience

## Description

Tokens from $get-ws-binding-token are meant only for binding a WebSocket to a Subscription, but they were audienced to the issuer like general access tokens, so they were also accepted on HTTP requests and on other WebSocket endpoints.

Binding tokens are now audienced to the WebSocket subscriptions URL. getLoginForAccessToken takes an optional expected audience, which the subscription notification path uses; every other caller keeps expecting the issuer and so rejects binding tokens.

Clients fetch a new binding token whenever they reconnect, so binding tokens issued before this change are replaced on the next reconnect.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `77ef9d16867a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.