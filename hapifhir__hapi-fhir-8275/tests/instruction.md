# Issue

**Title:** [8271] Fix ConcurrentModification error that happens randomly during …

## Description

### Issue

`CompartmentSearchParameterModifications` is populated once when an `AuthorizationInterceptor` rule list is built, then read concurrently by every thread evaluating that list. Both getters used `computeIfAbsent` on a plain `HashMap`, so a *read* for an unregistered resource type structurally modified the shared map — causing intermittent `ConcurrentModificationException` during batch requests. It also leaked one empty entry per resource type queried.

### For Code Reviewer

- Getters are now pure reads (`getOrDefault` → `Collections.emptySet()`), returning `unmodifiableSet`.
- Backing maps are `ConcurrentHashMap`; writes are copy-on-write inside `compute(..)`, so readers holding a previously returned `Set` never see it mutated. Chosen over a synchronized `Set` to keep reads lock-free; writes are build-time only and rare.
- Resource-type lookup normalizes with `toLowerCase(Locale.ROOT)` to avoid locale-dependent casing (e.g. Turkish `I`). Search parameter names stay case-sensitive, matching FHIR.

**Behaviour change:** the getters previously returned a live, mutable `Set` that callers could add to. That now throws `UnsupportedOperationException`. No such caller exists in this repo, but it is public API — downstream callers must use `addSPToIncludeInCompartment(..)` / `addSPToOmitFromCompartment(..)`. Noted in the changelog.

### For QA

1. Batch/transaction requests against a rule list using compartment SP modifications no longer intermittently fail with `ConcurrentModificationException` — verify under concurrent load, repeated runs.
2. Compartment authorization decisions unchanged: SPs added via `addSPToIncludeInCompartment(..)` still include, SPs omitted via `addSPToOmitFromCompartment(..)` still exclude.
3. Resource types with no registered modifications still use the stock compartment definition.
4. Resource type names match case-insensitively; search parameter names remain case-sensitive.
5. Repeated authorization evaluations do not grow memory over time.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0d7494bf98fa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.