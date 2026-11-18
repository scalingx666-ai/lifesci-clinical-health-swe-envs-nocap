# Issue

**Title:** Support child/parent "exists" filters and flat concept-property hierarchies in ValueSet expansion

## Description

## Summary

Enables expanding ValueSets that select concepts via the standard FHIR concept-properties with the `exists` operator — the hierarchical `child`/`parent`, the boolean `inactive`/`notSelectable`, and the date-valued `deprecated`/`deprecationDate`/`retirementDate` — for any terminology rather than only LOINC. It also builds the concept hierarchy from CodeSystems that express it FLAT (each concept referencing its parent/child via a `parent`/`child` concept-property) in addition to nested `CodeSystem.concept` arrays.

Motivating example: the German KDL terminology. Its ValueSet selects the leaf concepts via `filter: { property: "child", op: "exists", value: "false" }`, and its CodeSystem is published in both a flat and a nested representation. Neither expanded before this change (the child filter was rejected as LOINC-only — HAPI-0895 — and the flat hierarchy was ignored on store).

The standard properties are identified by their reserved code name. A property the CodeSystem declares with a non-canonical concept-properties URI (a different meaning) is not treated as the standard property.

## Changes

### In-memory (`ValueSetExpansionFilterContext`)

- Build the concept hierarchy from flat `parent`/`child` concept-properties (matched by their reserved code name), not only from nested concepts. This makes the existing structural filters (`is-a`, `descendent-of`, …) work for flat CodeSystems too.
- Handle `child`/`parent`, the boolean `inactive`/`notSelectable` (flagged only when the value is `true`), and the date-valued `deprecated`/`deprecationDate`/`retirementDate` (presence check) with `op = exists`, via one `StandardConceptProperty` registry.
- Resolve the hierarchy case-insensitively when the CodeSystem is not case-sensitive, and guard descendant traversal against cycles — including not reporting a concept as its own descendant.
- A property declared with a non-canonical URI is reported as an error (meaning unknown); an undeclared property is matched by name, with an info log the first time it is matched for a filtered property.
- Report an error (rather than a silently empty expansion) for a filter it cannot evaluate — a custom concept property, or a non-`exists` operator on the standard properties — so the caller can surface it or delegate to another terminology service in the validation-support chain.

### JPA (`TermReadSvcImpl`, `TermCodeSystemStorageSvcImpl`, `ITermConceptParentChildLinkDao`)

- `child`/`parent` + `exists` is now generic (no longer LOINC-gated), resolved from the parent/child links. The `exists` value is validated as a strict boolean.
- `inactive`/`notSelectable` + `exists` resolves value-aware against the indexed property (matches value `true`), rather than a plain presence check.
- `deprecated`/`deprecationDate`/`retirementDate` + `exists` is a value-aware presence check (so `exists=false` selects the complement); the date value itself is not interpreted and no schema change is involved.
- Flat `parent`/`child` concept-properties are turned into parent/child links when a CodeSystem is persisted, matched by their reserved code name (so an undeclared flat hierarchy is linked); a property declared with a non-canonical URI is skipped. Existing structural filters (`is-a`, `descendent-of`, …) work for flat CodeSystems since they rely on the same links.
- Works for any terminology; existing LOINC-specific parent/child/ancestor/descendant filters are unchanged.

**Migration note:** existing stored CodeSystems must be re-persisted/reindexed to pick up links from previously-undeclared flat `parent`/`child` properties.

## Testing

- `ValueSetExpansionFilterContextTest` — child/parent `exists` on nested and flat hierarchies; flat hierarchy matched by name (undeclared) and skipped for a conflicting URI; `descendent-of` on a flat hierarchy (incl. case-insensitive); cycle termination and no self-match; `inactive`/`notSelectable` and `deprecated`/`deprecationDate`/`retirementDate` `exists`; and unsupported property/operator or conflicting-URI now throwing.
- `InMemoryTerminologyServerValidationSupportTest` — an unsupported filter surfaces as an expansion error rather than a silent empty result.
- `FhirResourceDaoR4TerminologyTest` — `child exists=false` → leaves and `parent exists=false` → roots on a linked hierarchy; the same on flat (declared, **undeclared**, and non-canonical-URI) and nested CodeSystem resources; codes containing special characters; `descendent-of` on a flat resource; `inactive`/`notSelectable`/`deprecated` `exists`; and rejection of a non-boolean `child exists` value.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `83e977afb074`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.