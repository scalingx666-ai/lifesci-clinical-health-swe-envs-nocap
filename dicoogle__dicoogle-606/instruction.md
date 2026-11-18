# Issue

**Title:** Add opt-in `call-shutdown` setting to call plugin shutdown routines on Dicoogle shutdown

## Description

Although I was originally thinking about bringing the shutdown hook to call `shutdown()` on all plugin sets in Dicoogle 4, we felt that there was a need to have this earlier. This PR makes this capability _opt-in_, so that it does not require any breaking changes and does not lead to surprising behaviors.

.

- New server settings XML element `<call-shutdown>` in `<archive>`
   - if true, Dicoogle will call  `shutdown` on (not dead) plugin sets installed
   - this is false by default, but the plan is to make it true by default (opt-out) in Dicoogle 4, and maybe even deprecate it, so that in later versions the behavior becomes mandatory.
   - add test coverage for call-shutdown setting
- add shutdown hook to call  `PluginController.shutdown`
   - Although we've had issues with this when interoperating with Sentry, we currently believe that this functionality is more important than Sentry integration.
- improve `PluginController.shutdown()` by catching and reporting all exceptions individually

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d62289ebf730`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.