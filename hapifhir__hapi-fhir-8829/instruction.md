# Issue

**Title:** `$validate-code` not-found messages name the `CodeSystem` and `ValueSet` version used

## Description

### Fix

- `TermReadSvcImpl.validateCode` does a `CodeSystem` check: the version is looked up once and used both to find the code and to build the message, so the message names the version the code was actually looked for in. Before, the message did its own lookup and named only the URL.
- `TermReadSvcImpl.validateCodeIsInPreExpandedValueSet` does a pre-expanded `ValueSet` check: both not-found messages name the `ValueSet` with its version.
- The three not-found message texts move to `hapi-messages.properties`. The existing `unknownCodeInSystem` key keeps
  its name and gains a `ValueSet` placeholder, so custom message bundles still load.
- `getCurrentCodeSystemVersion` is now package-private so the unit test can stub it.
- Two changelog entries, one per message.

### Tests

- `ResourceProviderR4CodeSystemTest`:
  - no version requested: the message names the current version; an older version requested: the message names it.
  - current copy stored without a version: the message names the URL only.
- `TermReadSvcImplTest`: the message names the version the code was looked for in, even if another version became
  current meanwhile. Failed with a second lookup, passes now. The test setup now stubs the version lookup and the code query instead of `findCode`.
- `FhirResourceDaoR4ValueSetTest`: two `ValueSet` versions, URL without a version: both messages name `|2.0.0`. Failed before, passes now.
- `FhirResourceDaoR4ValidateTest`: one expected message updated, since `$validate` now shows the `ValueSet` URL.
- Ran: `TermReadSvcImplTest`, 12 r4 test classes (455 tests), 2 r5 classes, 3 dstu3 classes, `ChangelogFilesTest`. All pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `66a1375b5f6f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.