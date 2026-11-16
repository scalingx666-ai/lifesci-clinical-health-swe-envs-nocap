# Issue

**Title:** Fix self-hosted mode auth and default theme

## Description

## Summary
- Fix auth modal showing incorrectly in self-hosted mode by checking APP_MODE before requiring Valyu OAuth
- Set light mode as default by disabling system theme preference override

## Test plan
- [ ] Run app with `NEXT_PUBLIC_APP_MODE=self-hosted`
- [ ] Verify no auth modal appears on load
- [ ] Verify light mode is default theme

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7b161071e94f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.