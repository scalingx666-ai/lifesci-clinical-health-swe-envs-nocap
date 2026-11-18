# Issue

**Title:** feat(bots): honor Bot.rawBody on $execute and custom operations

## Description

- `Bot.rawBody` already worked on the anonymous public-webhook route but was never wired into the authenticated `$execute` operation or Bot-backed custom operations - both always used the pre-parsed body
- Replace the webhook-only raw-body parser in `app.ts` with a single `json()` parser on `BOT_EXECUTION_PATHS`: the webhook paths plus every FHIR `$operation` / `%24operation` path under each mount prefix (covers `$execute` and custom operations, which can't be distinguished by URL before routing). The captured buffer is stored on `res.locals.rawBody` instead of `req.rawBody`
- Add `getBotBodyInput` in `bots/utils.ts`, shared by the webhook handler, `$execute`, and `tryCustomOperation`: uses the raw body for POST when `Bot.rawBody` is set and a raw body was captured, falling back to the parsed body otherwise (including for non-JSON content types)
- `tryCustomOperation` takes the raw body as an optional argument, passed from the FHIR router; `$submit` re-dispatch doesn't pass it, and instance-level custom operations still receive the target resource
- Update the `Bot.rawBody` definition (and generated `fhirtypes`) and the webhook docs to cover `$execute` and custom operations
- Tests: raw vs parsed input for `$execute` (including non-JSON fallback) and for system- and type-level custom operations; webhook tests updated for `res.locals.rawBody`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fc3970ea385c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.