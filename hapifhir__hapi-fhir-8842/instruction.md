# Issue

**Title:** Let a bulk export job request terminology normalization

## Description

## For Code Reviewer

A bulk export job can now ask for terminology normalization in its own parameters. `BulkExportJobParameters` has a nullable `normalizeTerminology` Boolean, serialized with the job like `expandMdm`. The V3 export consumer translates a job's resources through `ResponseTerminologyTranslationSvc` when either the job parameter is `true` or the server-wide `NormalizeTerminologyForBulkExportJobs` storage setting is on. Nothing in this change sets the parameter: a server's own `STORAGE_PRE_INITIATE_BULK_EXPORT` hook does, per request.

Points that need a closer look:

- The parameter is an opt-in, not an override. `null` and `false` both leave the storage setting in charge, so a job with `false` still translates when the server-wide setting is on. The consumer tests cover each arm of that gate.
- The field is annotated `@JsonProperty` because the job's parameters are stored as JSON and read back by the worker. The job-reuse lookup compares the serialized parameters too, so a translated export does not reuse an untranslated job, or the reverse.
- A job that asks for normalization on a server with no `ResponseTerminologyTranslationSvc` bean still fails with HAPI-3053, as the storage setting already does. The message now names what asked for normalization.
- The V2 export step is deliberately unchanged. New jobs start on V3, and V2 only completes jobs that were already running when the server was upgraded. A V2 job ignores the parameter.
- Possible follow-up, not part of this change: the hook that sets the parameter could instead live on the base `ResponseTerminologyTranslationInterceptor` in `hapi-fhir-server`, so servers that use that interceptor would get the behaviour without a hook of their own.

## For QA

The tests cover the gate in `ExpandResourcesConsumerTest`, and a real V3 bulk export job with the parameter set and the storage setting off in `ResponseTerminologyTranslationInterceptorTest`. What they do not reach is the `$export` request path on a running server:

- [ ] With a mapping added through `ResponseTerminologyTranslationInterceptor#addMappingSpecification` and the storage setting off, a `$export` whose `STORAGE_PRE_INITIATE_BULK_EXPORT` hook sets `normalizeTerminology` to `true` returns the translated codings in the exported Binary files. Check each export style.
- [ ] The same `$export` with the hook leaving the parameter unset returns the source codings only.
- [ ] With the storage setting on, exports are translated whether or not the hook sets the parameter.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b162911032e0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.