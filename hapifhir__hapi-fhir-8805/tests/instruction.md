# Issue

**Title:** Terminology upload, SNAPSHOT over existing version, $lookup returns the CodeSystem URL as name

## Description

## For Code Reviewer

A SNAPSHOT upload over an existing code system version stored the code system URL as the version's display name, so `CodeSystem/$lookup` returned the URL as `name`. Two places contribute:

- The `content: not-present` branch of `TermCodeSystemStorageSvcImpl.storeNewCodeSystemVersionIfNeeded` passed the URL as the `TermCodeSystem` name. That has been there since 2020 and was harmless, because `$lookup` never read that name.
- Since the Batch2 staging rewrite (HAPI 8.12.0), `startStagingCodeSystemVersion` copied `TermCodeSystem.name` into the new version's display name, which made the URL visible to `$lookup`.

The fix uses the uploaded `CodeSystem.name` in both places. The staging method takes the display name as a third parameter, passed from `BaseExpandDistributionIntoFilesStep`. A blank name falls back to the stored name.

Points that need a closer look:

1. **Both changes are needed.** Fixing only the not-present branch leaves databases where the stored name is already the URL. A later SNAPSHOT whose write is a no-op would still stage that URL.
2. **The not-present branch runs only on a real change.** Under default `VERSIONED` tag storage, an identical `codesystem.json` re-upload is suppressed as unchanged, so the bug stays hidden there. The new tests cover an edited `codesystem.json`, `INLINE` tag storage, and an identical re-upload over a row already named with the URL.
3. **API change.** `ITermCodeSystemStorageSvc` gains an abstract three-argument `startStagingCodeSystemVersion`. The two-argument form stays as a `@Deprecated(since = "9.2.0")` default that passes `null`. `TermCodeSystemStorageSvcImpl` is the only implementation in the repo, but external implementers of the interface must add the new method.
4. **Nameless uploads change behavior.** A SNAPSHOT whose `codesystem.json` has no name now gives no `$lookup` name, where it used to give the URL. This is deliberate: the URL was never a name, and restoring it as a fallback would bring back the disagreement between the two paths.
5. **Existing data is not migrated.** A version already stored with the URL as its name stays that way until the code system is uploaded again as a SNAPSHOT. ADD and REMOVE deltas do not change the name. The upgrade note in `hapi-fhir-docs/src/main/resources/ca/uhn/hapi/fhir/changelog/9_2_0/upgrade.md` says so. A docs-only CDR MR carries the matching note and follows this merge.
6. **Log arguments.** Three log calls in `TermCodeSystemStorageSvcImpl` had their `url` and `version` arguments swapped. They are corrected; there is no behavior change.
7. **Outside this PR, possibly a separate HAPI issue.** Under `INLINE` tag storage, the first job write after a create is stored as a new version (`_history/2`) even when the `CodeSystem` content is identical, instead of being suppressed as unchanged. This PR does not change that. It may be worth its own issue.

## For QA

The new tests in `TerminologyLoaderSvcCustomJpaTest` and `TermCodeSystemStorageSvcImplTest` check the `$lookup` name and `TermCodeSystem.name` at the JPA level, through the staging path.

Acceptance criteria the tests cannot reach:

- [ ] **Setup:** a CDR build that consumes this HAPI build, on a server with `tag_storage_mode=INLINE`. Upload a custom terminology `labCodes|1.0` as an ADD, then upload it again as a SNAPSHOT through the CDR upload CLI, which uses the real zip path. `GET CodeSystem/$lookup?system=http://example.com/labCodes&code=HB` returns the name `Example Lab Codes`.
- [ ] Upload the same code system through the REST terminology upload job (create job, attach file, start job). The test helper skips those calls, so this path is not covered by the tests.
- [ ] On a database where `$lookup` already returns the URL as `name`, a SNAPSHOT upload with this build corrects it. An ADD delta on the same database does not.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8eafcdb9ad1a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.