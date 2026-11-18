# Issue

**Title:** profile: write the record by code, ask the model only for its scenario

## Description

## What was wrong

After every ingest, `mirobody/user/profile.py` asked a model to **rewrite the whole health profile**: the previous profile, every new reading, and every value of the past three years ("Ensure all available data is included"). The cap was 32,000 tokens "to avoid truncation". With MiniCPM5-2B on the llama.cpp router (100%-local mode), this went wrong in several ways:

- **It ran away.** In one local load it wrote all 32,000 tokens three times, 18–21 minutes each on a GPU. The 600 s timeout freed the lock while the server kept writing, so the next refresh took the router's other slot.
- **It copied the record wrongly.** Replayed from that load's database, it filed a urine glucose under 血糖 and NEUT% under 电解质. It then wrote `- 尿酸: 无记录` lines for panels the person never had and cycled through them to the cap: 204 lines, only 70 of them distinct.
- **It copied its instructions.** Two of the seven profiles it stored opened with the template's Core Summary paragraph. That section is what the agent's system prompt carries.
- **It read its own last version,** so whatever one rewrite got wrong, the next one kept. `kernel/memory.py` exists to rule that out.
- **No scenario got through.** Asked for a `## 场景` heading, an empty line and the name, it wrote the heading and stopped. Every profile in that load's database has the default scenario.

The first version of this PR capped output at 6,144 tokens and refused to store a cut or echoed profile. That bounded the damage, but the runaway still happened, and a refused refresh left the profile behind its readings.

## What changed

**Code writes every section from the record; the model only picks the scenario.**

- **Code renders the record.** It reads through `PostgresHealthQuery.records`, the read the tools and the Data page use:
  - the core summary: sex and age; conditions and findings the report marked abnormal; readings outside their printed range; symptoms reported more than once;
  - then each reading with its range and flag, the findings, the symptoms and the device week.

  It covers the past three years, plus any diagnosis however old. The section headings are unchanged.
- **The model is asked one thing:** one line, `场景：<name>`, with `max_tokens` 1024. A name not in the table is not stored. If there is no answer, the previous scenario stays, so the profile is stored even with no model configured.
- **The previous profile document is no longer read.** This closes the roadmap item about the rewrite feeding on its own output.
- **Removed:** `CutAtMaxTokens`, `whole=`, the echo check and the `rejected` status. Nothing the model writes is stored except a name from a closed table. Replies cut at `max_tokens` are still logged on both backends.
- **Kept:** `timed_out` stays, and is still not retried.

Smaller asks were tried first on the same 17 replayed refreshes, and both failed:

| Ask | Result |
|---|---|
| Write the summary alone, from a digest code built | It no longer looped, but filed symptoms as conditions, left out sex and age, called in-range values "elevated", and once turned a prompt sentence into a bullet label. |
| Fill in short labels | Two people got the labels back empty. |

Every fact the summary needs was already sorted by code, so code writes it.

## Measured (MiniCPM5-2B Q8_0, `docker/local-models.ini`, Apple GPU)

| | tokens the model wrote | seconds | profile stored |
|---|---|---|---|
| Before: one person's two refreshes side by side on a fresh router (looped 2 of 2) | 32,000 | 2,220 | no: the client gave up at 1,800 s and the server wrote 420 s more |
| Before: the same pair once the prompts were cached | 916 / 3,266 | 61 / 190 | yes, both opening with the prompt's instructions |
| This PR's first version, same fresh-router pair | 6,144 (cut) | 1,316 | no (rejected) |
| **After: same fresh-router pair, run twice** | **4 / 4** | **15** (incl. model load) | **yes** |
| After: all 17 replayed refreshes | 4–12 | 0.3–3 | yes |

## How to tell

- The profile's lab section quotes each reading as it is stored.
- The worker no longer spends minutes per refresh.
- `profile scenario not picked, previous kept` is logged when the model names no scenario.
- `text completion hit max_tokens` is logged for any cut reply.

## Tests and gates

`mirobody/tests/test_profile_from_record.py` (20 tests):
- A model that never stops writes one capped answer and the profile is still stored, scenario kept. Same for no model at all.
- A model that repeats its prompt gets none of it into the profile.
- A scenario name not in the table is not stored.
- No statement reads the previous document.
- The core summary lists only what is abnormal or recurring, in Chinese for a Chinese speaker, and counts what it leaves out.
- An old diagnosis is kept; an old reading is not.
- `timed_out` is not retried; `error` is.
- A cut reply is logged on both backends.

Gate results:
- `ruff check mirobody examples`: clean
- `compileall`: ok
- `lint-imports`: 6 kept, 0 broken
- bare library import: ok
- comment style: 0 problems
- PHI log lint: 0 new findings
- `pytest -q`: 1260 passed, 121 skipped, 12 xfailed (two files from main that need `quickjs_rs`, absent from my venv, set aside; CI runs them)
- minimal install: the module is skipped

No library-layer module was added. Only the English CHANGELOG changed; no README text changed.

**Known and left alone:**
- On the 2B the scenario choice itself is weak; one of the five people got 糖尿病患者并发症防控 with no diabetes on record. Nothing in this repository reads the scenario column.
- WebSocket uploads still refresh twice.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a58ba061f4ca`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.