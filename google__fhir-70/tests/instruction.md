# Issue

**Title:** Accept PackageManagers When Constructing LocalFhirPathContexts

## Description

Accept PackageManagers When Constructing LocalFhirPathContexts

- Expect to receive structure definitions in FhirPackageManager (or FhirPackage)
  objects rather than resource collections. This allows the context to retrieve
  resources defined in multiple packages. This is required for validation
  workflows (and likely others!)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f595f9495482`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.