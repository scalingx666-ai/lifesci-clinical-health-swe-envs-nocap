# Issue

**Title:** Questionnaire v2: one header per structured question + rendering coverage for all types

## Description

**Stack 6/6** — chain: #16618 ← #16627 ← #16628 ← #16629 ← #16630 ← **this**.

## Alignment fix

On the v2 fill page every structured question rendered **two headers**: the renderer's block header ("1. Symptom \*") and the widget's own internal `QuestionLabel` right under it — differently styled, ~30px off the block's left edge, with the label's indigo ornament bar floating between them.

The legacy fill stack that needed the internal label is deleted and the v2 adapters are these widgets' only consumers, so the widgets drop it: all 11 `QuestionTypes/*` components now render content only, the renderer's numbered header is the single header, and history/template affordances keep a right-aligned row. `QuestionLabel` itself became dead code and is deleted (v2 README allowlist updated).

| Before | After |
|---|---|
| `1. Symptom *` ⟶ ornament bar ⟶ `Symptom *` (misaligned) ⟶ table | `1. Symptom *` ⟶ table (history button right-aligned) |

## Structured rendering coverage for all 11 types

Existing structured specs cover CRUD for 5 types (symptom, diagnosis, allergy, medication request, charge item) — six types had no fill-page coverage at all. New `structuredRendering.spec.ts` parametrizes over **every** core type via its fixed questionnaire (symptom, diagnosis, allergy_intolerance, medication_request, medication_statement, service_request, encounter, files, time_of_death, charge_item, appointment) and pins per type:

- the widget mounts a real, visible input — none of the slot's degradation notices show,
- exactly **one** question header renders (the duplicated-label regression),
- the form canvas has no horizontal overflow (layout smoke).

## Verification

- All 11 rendering tests green; structured CRUD + fill + medicine + service-request regression suites green (60 passed; the one failure is the pre-existing `diagnosis.spec.ts` flake that fails on a different test each run, tracked separately).
- `tsc`, ESLint and Prettier clean.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4c6a9d07eef2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.