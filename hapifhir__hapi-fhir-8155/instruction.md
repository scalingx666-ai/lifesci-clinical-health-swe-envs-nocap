# Issue

**Title:** 8035 backward compatibility of infer system param for R4 validation

## Description

The `inferSystem=true` parameter added to remote terminology `$validate-code` requests in 8.10.0 (#7616) was sent for **all** FHIR versions whenever a code's system could not be determined locally. `inferSystem` is an R5+ `$validate-code` parameter, so strict R4/DSTU3-compliant remote terminology servers (e.g. VSAC, CMS) that don't recognize it rejected these requests, breaking validation that had worked before 8.10.0.

### Fix

- **RemoteTerminologyServiceValidationSupport** — `inferSystem=true` is now only sent for R5 and newer FHIR contexts by default, gated by a new `shouldInferSystem(FhirContext)` check. R4/DSTU3 contexts no longer send the parameter, restoring compatibility with strict R4 servers.
- **New `setInferSystemEnabled(Boolean)` toggle** — provides an escape hatch to override the default: `null` (default) sends it only for R5+, `TRUE` always sends it (e.g. for an R4 server that does support inference), and `FALSE` never sends it.

### Tests

- `RemoteTerminologyServiceValidationSupportR4Test` — updated to assert an R4 context does **not** send `inferSystem` by default, plus a new test verifying `setInferSystemEnabled(true)` forces it to be sent.
- `RemoteTerminologyServiceValidationSupportR5Test` — new test (with a stub `$validate-code` provider) verifying an R5 context still sends `inferSystem` by default.

### Docs

- New "Inferring the Code System" section in the RemoteTerminologyServiceValidationSupport validation-support-modules docs describing the R5+ default and the `setInferSystemEnabled` toggle.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a246dbd4e6b8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.