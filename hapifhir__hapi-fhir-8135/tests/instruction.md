# Issue

**Title:** Pin hapi-fhir-typescript to Node 16.20.2 (stopgap)

## Description

## Summary

The CDR "Compile against CDR" check has been failing on every PR since `hapi-fhir-typescript` was introduced (#8118) because the module pins Node `v24.18.0`, and CDR's CI runner (`hdp-ci-maven`, Amazon Linux 2, glibc 2.26) can't execute Node 18+ prebuilt binaries, which require glibc >= 2.28. `npm install` fails immediately because Node itself can't start:

```
node: /lib64/libc.so.6: version `GLIBC_2.28' not found (required by node)
```

## Fix

Pin `ts.node.version` to `v16.20.2`, the last Node 16 LTS release, which runs fine on glibc 2.26.

This is a **stopgap**. The real fix is upgrading the CI runner's base image. Amazon Linux 2 itself reached end-of-support on 2026-06-30. Bump this pin once that lands.

## Test plan

- [x] Verified locally against the actual `registry.gitlab.com/simpatico.ai/cdr/hdp-ci-maven:3.9-amazoncorretto-21` image via Docker, using the exact CI invocation (`mvn --batch-mode --errors clean install -q -P DIST -Dmaven.test.skip`) - `BUILD SUCCESS`.
- [x] Confirmed Node `v18.20.4` reproduces the exact glibc error seen in CI on that same image; `v16.20.2` does not.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `40d428bc0268`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.