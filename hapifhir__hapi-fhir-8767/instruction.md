# Issue

**Title:** Fix pre-expansion for `ValueSet` includes and excludes that name a `CodeSystem` version

## Description

### Problem
With full-text indexing off, pre-expanding a `ValueSet` whose include or exclude names a `CodeSystem` version stored the system as `url|version`. `$validate-code` then rejected valid codes, and a versioned exclude left its codes in the expansion.

### Scope
This pull request fixes new expansions. Expansions stored before the fix stay wrong until the `ValueSet` is re-expanded, for example with `$invalidate-expansion`. An automatic repair solution is implemented as a fast-follow in 

### Root Cause
`Step2And3ExpandConceptsStep.ChunkingAccumulator` introduced in #8127 stores the system in the pre-expansion tables as `url|version` since that is what is passed in the system parameter. 

### Fix
Instead of fixing the stored value, we can now fix the value of system by leveraging new APIs with the separate version added as part of #8402. For a clean fix, we need to propagate a similar API change in `IValueSetConceptAccumulator`.

### Changes
- `TermReadSvcImpl` passes the plain URL and the version separately.
- Versioned excludes now match on system, version and code.
- Made some API changes to `IValueSetConceptAccumulator`, not breaking, following the same pattern as `IValidationSupport` in #8432. Added a changelog entry for it.
- The new `excludeConcept` is a `default` method that calls the old two-argument one, so existing implementations keep working.
- The old `excludeConcept(String, String)` is `@Deprecated(since = "9.0.0")` and still abstract, so the two methods cannot call each other forever.
- `includeConceptWithDesignations` now always gets the plain URL; a custom accumulator that parsed `url|version` from `theSystem` should read `theSystemVersion`.
- Pre-expansion removes only the named version's codes for a versioned exclude (TermValueSetStorageSvcImpl.removeConceptsFromExpansion)
- `$expand` before pre-expansion applies the same rule, so both give the same result; the rule lives in `TermReadSvcUtil.excludeAppliesToVersion`.
- Codes stored without a version still match a versioned exclude: with full-text indexing off, an include that names no version stores its codes without one.
- Small side effect (fix): a concept with a blank system or code is now skipped on the unversioned path too; before, only the versioned path skipped it. 
- Small side effect (fix): with full-text indexing on, `$expand` of a `ValueSet` that includes the same code from two versions now lists it once per version, as it already did without full-text indexing.

### Testing
- `FhirResourceDaoR4ValueSetTest`: new test, full-text indexing on and off; fails without the fix (system `url|1.0.0`, excluded code kept).
- `FhirResourceDaoR4ValueSetTest`: an exclude that names another version than the include keeps the include's code, before and after pre-expansion.
- `FhirResourceDaoR4ValueSetTest`: an include without a version and an exclude naming the installed version; the excluded code is removed from `$expand` before pre-expansion and from the stored expansion, and rejected, full-text indexing on and off.
- `IValueSetConceptAccumulatorTest`: a versioned exclude removes a code added without a version, which can then be added again.
- `IValueSetConceptAccumulatorTest`: the default method and the deprecated form.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8b6d2d79ba8e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.