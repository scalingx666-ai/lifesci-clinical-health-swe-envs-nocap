# Issue

**Title:** fix(deps): override tinypool to 2.2.0

## Description

Fixes the critical `npm audit` findings for `tinypool` (GHSA-5gmw-xhrv-c9v3, GHSA-85c8-ppgw-ccpr: prototype pollution leading to RCE, fixed in 2.1.2).

`tinypool`'s only consumer is `@docusaurus/core` (via `packages/docs`), which pins `^1.0.2`, so `npm audit fix` can only offer a breaking Docusaurus downgrade. This adds a root `overrides` entry pinning `tinypool` to 2.2.0.

The only breaking change in tinypool 2.0 is dropping Node 18 ([release notes](https://github.com/tinylibs/tinypool/releases/tag/v2.0.0)); the repo requires Node 22 or 24.

## Testing
- `npm audit`: critical goes from 16 to 0 (remaining highs are unrelated packages)
- Ran a Tinypool pool with Docusaurus's exact SSG constructor options (`isolateWorkers: false`, `maxMemoryLimitBeforeRecycle`, `workerData`, `__tinypool_state__.workerId`) on 1.1.1 and 2.2.0; identical behavior
- CI's docs build exercises the real SSG path

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2f583b2aa78d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.