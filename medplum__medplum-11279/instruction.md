# Issue

**Title:** fix(server): Return 400 for exposed client errors such as bad compressed bodies

## Description

A request with Content-Encoding: br and a body that isn't valid Brotli makes body-parser fail with a 400 http-error that has no `type`, so the global error handler logged it as unhandled and returned 500.

The `http-errors` package sets `expose` on errors whose message is safe to return to the client (any status below 500). When an exposed error has status 400, we now return its message to the client in a 400 badRequest outcome.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d9e22944fd5b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.