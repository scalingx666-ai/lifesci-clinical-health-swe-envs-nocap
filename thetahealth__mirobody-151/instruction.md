# Issue

**Title:** translate: curate 40 everyday English S-axis surfaces

## Description

## What

Adds 40 curated rows to `mirobody/res/icpc3/symptoms_en.tsv` so common lay
English symptom phrasings resolve on the ICPC-3 S (symptom) axis. No
resolver code change (`mirobody/translate/icpc3.py` untouched).

## Why

Measured 2026-10-14 against `mirobody.translate.icpc3.resolve_symptom` on
main: phrasings such as "neck pain", "palpitations" and "stomach ache"
returned `needs-input` / `icpc3:no-match`, although a close variant already
curated ("stiff neck" -> LS01, "heart racing" -> KS02) made the intended code
unambiguous. Added surfaces and their codes:

| Surface | Code | Surface | Code |
|---|---|---|---|
| chest hurts | AS12 | headaches | NS01 |
| sweating a lot | AS10 | tingling fingers | NS04 |
| sweaty | AS10 | shaky | NS07 |
| stomach ache | DS02 | trembling hands | NS07 |
| stomach pain | DS02 | anxious | PS01 |
| mouth feels dry | DS20.00 | nervous | PS01 |
| dry eyes | FS07 | irritable | PS04 |
| tinnitus | HS03 | stressed out | PS02 |
| buzzing in my ears | HS03 | sleeping badly | PS06 |
| palpitations | KS02 | coughing | RS07 |
| neck pain | LS01 | sneezing | RS09 |
| sore neck | LS01 | coughing up phlegm | RS15 |
| back pain | LS02 | phlegm | RS15 |
| knee pain | LS14 | itching | SS02 |
| shoulder pain | LS07 | hair loss | SS10 |
| joint pain | LS20 | hair falling out | SS10 |
| aching joints | LS20 | not hungry | TS03 |
| lost my appetite | TS03 | dropping weight | TS07 |
| gaining weight | TS06 | really thirsty | TS01 |
| weeing a lot | US02 | needing to pee all the time | US02 |

`stomach ache`/`stomach pain` -> DS02 follows the maintainer note already in
the file ("ICPC-3 files the literal 'stomach ache' under DS02, epigastric");
DS02's own inclusion list carries the literal (slash-joined) phrase
`stomach ache/pain`, which could not match user input directly. `back pain`
-> LS02 follows the same evidence: LS02's inclusions list the unqualified
`backache`, while LS03's are all explicitly lower-back terms.

## Deliberately not added

- `swelling`, `puffy` — genuinely ambiguous between AS09 (generalized) and
  KS04 (ankle specifically, or the face); no site named.
- `numb hands` — NS04 is "tingling fingers, feet, toes" (digits); NS05
  ("sensation disturbances") explicitly excludes "tingling fingers/feet/toes",
  implying NS05 covers numbness of the hand as a whole. Added `tingling
  fingers` only, which is unambiguous.

Checked every addition against `terms()` for a conflicting preferred/
inclusion match before adding it; none existed (verified with `_lookup`).

## How verified

- `mirobody/translate/icpc3.py` unchanged; `uvx ruff check mirobody`,
  `lint-imports` (6/6 contracts kept), `scripts/check_comment_style.py
  mirobody` (0 problems) all pass.
- New `tests/translate/test_icpc3_lay_english.py` (gitignored local suite):
  68 cases — all 40 additions code correctly, the variant each sits next to
  is unaffected, surfaces already reachable via ICPC-3's own preferred/
  inclusion tiers needed no row, and the deliberately-ambiguous/bare terms
  still abstain.
- `tests/translate/test_icpc3_axes.py` (41 tests, including the
  `eval/icpc3_cases.tsv`-backed wrong-rate gate) and `mirobody/tests/
  test_skills.py` (incl. `test_icpc3_examples`) both pass unchanged.
- `python -m pytest tests/translate mirobody`: 870 passed, 101 skipped, 12
  xfailed, 4 pre-existing failures (SQL aggregator threshold parsing,
  `windows.all_windowed_names`, a `[degF]` conversion bound) confirmed to
  reproduce identically against the unmodified `symptoms_en.tsv` from
  `origin/main` — unrelated to this change.
- `scripts/stamp_bundle_version.py --check` passes (it only stamps the LOINC
  bundle tar; ICPC-3 resources are outside it).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f4fcee681b3a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.