# Issue

**Title:** Upgrade Windows functional test pool to windows-2025

## Description

This updates the Windows functional test job to use the `windows-2025` hosted image in `build/run-functional-tests.yml`, aligning the pipeline with the required VM image upgrade.

- **Functional test pool**
  - Changed the `Windows_Functional_Test` job pool from `windows-2019` to `windows-2025`
  - Left the OSX job and all functional test steps unchanged

- **Workflow scope**
  - Limited the change to the shared functional test pipeline template used by the build definitions
  - No production code or test logic changed

```yaml
- job: Windows_Functional_Test
  pool:
    vmImage: 'windows-2025'
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7b0d02dab73e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.