# Issue

**Title:** Update org.hl7.fhir.core to 6.10.4

## Description

Updates org.hl7.fhir.core from 6.10.3 to 6.10.4, and handles the one behaviour change it brings for HAPI servers. If this builds cleanly, a 6.10.4.1 special release from core's `rel_6_10_4_1` branch, with validator performance fixes (hapifhir/org.hl7.fhir.core#2833–#2840), will follow in a separate PR.

### Changes

- `fhir_core_version` 6.10.3 → 6.10.4. Nothing else needed to change to compile.
- `NpmPackageValidationSupportTest.testValidateIheMhdPackage` expects 5 messages, not 4. The new one is 6.10.4's information message `TYPE_SPECIFIC_CHECKS_DT_ATT_URL_NOT_A_LINK`: the document's Attachment points at a `urn:uuid`, so its content isn't checked. The test now asserts it.
- Conditional references outside a transaction: see below.

### Conditional references outside a transaction

Core 6.10.4 fixed hapifhir/org.hl7.fhir.core#2474, where the validator threw a `StringIndexOutOfBoundsException` on a conditional reference such as `Observation?identifier=...`. As part of that fix it added a rule, `REFERENCE_REF_QUERY_NOT_TRANSACTION`: a conditional reference is an error unless the resource is inside a transaction Bundle. That's what the FHIR specification says, and core master (7.x) has the same rule.

HAPI FHIR JPA servers also resolve these references on a plain create or update when inline match URL references are allowed (`StorageSettings.allowInlineMatchUrlReferences`, default true). So with request validation on, such a request is now rejected, where #6316 had made it pass.

As with earlier core changes to message severity, this PR accepts core's rule and gives servers an opt-in way to change the severity:

- **`testValidateConditionalReferenceWithChain`** (from #6316) now expects the `REFERENCE_REF_QUERY_NOT_TRANSACTION` error.
- **New `ValidationMessageConditionalReferencePostProcessingInterceptor`** in `hapi-fhir-server`. Like `ValidationMessageUnknownCodeSystemPostProcessingInterceptor`, it is a `ValidationMessagePostProcessingInterceptor` with a single rule on that message id. By default it reports these references as warnings; a constructor takes another severity. The new `testValidateConditionalReferenceWithChainIsDowngradedByInterceptor` covers it.
- **Docs:** a section in `instance_validator.md` with a `ValidatorExamples` snippet, a changelog entry, and an upgrade note in `9_2_0/upgrade.md`.

The interceptor is opt-in: HAPI doesn't register it automatically when inline match URLs are allowed. The other severity interceptors work the same way.

Note for reviewers: `ValidationResult.isSuccessful()` is computed once, when the result is constructed. So after any post-processing interceptor downgrades an error it still returns false. `RequestValidatingInterceptor` and `$validate` decide from the message severities, so they aren't affected. This is existing behaviour, left alone here.

### Local results

hapi-fhir-validation: 1377 tests, 0 failures. `hapi-fhir-docs` (the new snippet) wasn't compiled locally.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

MB: I've tagged it as ai-generated, but have read every line.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `852fe5fa7261`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.