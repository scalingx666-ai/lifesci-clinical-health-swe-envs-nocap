# Issue

**Title:** translate: a complaint does not answer a LOINC code

## Description

`mirobody resolve 发烧` returned 103717-5, a Crimean-Congo haemorrhagic fever
virus RNA assay. A complaint or a diagnosis came back as a test FOR the thing:
an organism assay, an antibody, a gene panel, a drug level, a risk score, or an
observation about somebody else ("Fever in Mother", "in Vomitus", "History of").

## What changed

- **88 curated complaints and diagnoses** across English, Russian, Japanese and
  Chinese are deliberate refusals in `resolver_overrides.tsv`
  (`<surface>\t!unresolved`). Classified by reading each returned canonical name
  one at a time, not by a regex: the failure is semantic, so a pattern that
  separated a test from its disease would have to know what every code measures.
- **`mirobody resolve` prints where to look** rather than a wrong code. A refused
  term names the ICPC-3 complaint axis and the flag that reaches it.
- **`--symptom` / `--condition`** resolve on that axis,
  (`resolve_symptom` / `resolve_condition` in the library).

```
$ mirobody resolve 发烧 血红蛋白
  发烧      unresolved: not a lab analyte. This is a complaint: ICPC-3 AS03 (Fever). Ask with --symptom.
  血红蛋白  LOINC 718-7       Hemoglobin [Mass/volume] in Blood   [65 candidates]

$ mirobody resolve --symptom 发烧
  发烧  ICPC-3 AS03       Fever
```

## Verification

- `tests/test_resolver_refusals.py` pins all 88 refusals and 15 terms that must
  **keep** resolving with the same code, plus the four CLI behaviours.
- The release gate and the resolver-table gate: **412 passed**.
- Checkup-panel coverage unchanged at **296/296**; the eval cases do not move
  (0.916 resolved, 0.969 covered, 0.030 wrong).

## Two judgment calls, recorded

- **`ache` also refuses `AChE`** (acetylcholinesterase, 1710-3). An appended
  `AChE` row cannot win, because `_is_blocked` flattens every surface variant and
  `AChE`/`ACHE`/`ache` all reach `ache`. Accepted: the enzyme has
  `acetylcholinesterase` spelled out. Recorded in the test module.
- **`水痘` now refuses**, shadowing the curated `水痘 → Varicella zoster` row.
  Correct: a varicella-zoster DNA assay is a test for the diagnosis, not the
  diagnosis. The ICPC-3 axis codes it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `49aa6d31281e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.