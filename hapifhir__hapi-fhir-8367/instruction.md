# Issue

**Title:** Evaluate custom concept-property filters on content=complete CodeSystems

## Description

.

## Problem

In-memory ValueSet expansion never evaluated a filter that selects on a custom
`CodeSystem.concept.property`, such as the LOINC `SCALE_TYP` filter the core `doc-typecodes`
ValueSet uses. It returned a hard failure instead, with `HAPI-3004`. But `content: complete` asserts
that the CodeSystem carries every concept it defines, so when such a CodeSystem is supplied inline
and the concept carries the property value, the expansion already holds every input the filter
needs. The evaluation is feasible without any terminology backend, and is what should happen in
place of a rejection.

This is not a regression in capability. Before 8.12 the same case returned a fabricated "not a
member" for a filter that was never evaluated; the resulting empty expansion was reported as
`not-in-vs`, which the validator discards unconditionally. As a result, a check that never ran
silently passed. #8181 replaced that with an explicit failure. This PR implements the missing
capability rather than reverting it.

## Change

All of it applies only when `CodeSystem.content == complete`.

**`ValueSetExpansionFilterContext`**

- Indexes custom `CodeSystem.concept.property` values for the property codes the ValueSet filters
  reference.
- Evaluates the filter for operation (`ConceptSetFilterComponent.op`) `=`, `in`, `not-in` and
  `regex`. The structural operators (`is-a`, `descendent-of`, `child-of`, …) resolve against concept
  codes and remain unsupported.
- Adds `UndeterminedFilterException`, raised when membership can be neither established nor ruled
  out.

**`InMemoryTerminologyServerValidationSupport`**

- Maps `UndeterminedFilterException` to a `not-found` issue (`Msg.code(3049)`), beside the existing
  `UnsupportedFilterException` → `vs-invalid` mapping.

## Behaviour

Validating `http://loinc.org|29550-1` against a filter of `SCALE_TYP = Doc`, with
`content: complete`:

| `CodeSystem.property[]` | concept's value | determination | result |
|---|---|---|---|
| declares `SCALE_TYP` | `"Doc"` | matches | validates |
| declares `SCALE_TYP` | `"wrong"` | does not match | `not-in-vs` |
| declares `SCALE_TYP` | absent | no value, so not a member | `not-in-vs` |
| undeclared | `"Doc"` | matches | validates |
| undeclared | `"wrong"` | does not match | `not-in-vs` |
| undeclared | absent | cannot be made | `not-found` |

Before this change every row produced `HAPI-3004`. Five of them now reach a real determination; the
last still cannot be determined, and what changes there is how that is reported. It previously
produced `vs-invalid`, which is fatal at every binding strength and blocks a client on a condition
it cannot remedy. It now produces `not-found`, whose severity gets recalculated from the binding
strength: `WARNING` for `extensible` and `preferred`, and `ERROR` for `required` when the issue
concerns an HL7 system or `unknownCodeSystemsCauseErrors` is set. A `preferred` binding is therefore
no longer blocked, but the client is still told the check could not be completed.

## Testing

`InMemoryTerminologyServerValidationSupportTest` covers the six rows end to end through
`validateCodeInValueSet`; `ValueSetExpansionFilterContextTest` covers the filter context directly,
including the other operators and a guard proving the gate is on the content mode rather than on the
data being present. Full `hapi-fhir-validation` module: 1190 tests green.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1e4aa0103171`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.