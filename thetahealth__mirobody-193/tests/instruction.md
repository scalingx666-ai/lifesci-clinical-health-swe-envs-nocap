# Issue

**Title:** docs: open with mirobody.ai's definition of Mirobody

## Description

## Why

mirobody.ai is the canonical definition of Mirobody, and it makes **the record** the product:
- the title is *Mirror Your Body in Data*, or 「你的健康数字分身」 in Chinese;
- the hero line is *One standard, every source, one complete picture of you — building a lasting record to understand where your health is going*;
- the record is called *your Mirobody*.

GitHub, PyPI and Docker Hub opened with the answer instead: *Turn scattered health data into answers you can trace* and *AI health data engine*.

## What changes

| Where | Before | After |
|---|---|---|
| README tagline | Turn scattered health data into answers you can trace. | **Mirror your body in data.** (中文：你的健康数字分身。日本語：あなたのからだを、データに映す。) |
| README line 1 | A self-hosted AI health data engine that brings … into one standardized record. | mirobody.ai's hero line, quoted as written |
| README line 2 | — | What this open-source edition does: it builds the record on your own machine, traces every number to its source, and gives your agent access over MCP |
| README line 3 | the three ways to start | unchanged |
| PyPI summary | Self-hosted AI health data engine: … | Mirror your body in data: one standardized, self-hosted record of … |
| Docker Hub | same as the old tagline | same order as the README |

The English and Japanese end lines now name the hosted app **Theta**, as mirobody.ai and thetahealth.ai do (owner, 10-27), and carry two live badges. The badges read Theta's public stats endpoint, the same one mirobody.ai's proof bar polls, and show registered and daily-active users. The Chinese README is left as it is.

## After merge (not in this PR)

The GitHub **About** text has no file, so it changes by hand. Proposed text:

> Mirror your body in data. One standard, every source, one complete picture of you: a self-hosted health record built from lab reports, wearables and genetics, with every number traced to its source and a built-in MCP server. Run it with Docker and one LLM key, or keep every model local on llama.cpp.

## Verified

- The docs site's `facts.mjs` patterns still match all three editions: the tagline under `# Mirobody`, and three stage rows.
- No first screen names LOINC or UCUM.
- `test_skills.py`: 85 passed.
- GitHub's renderer (`mode=markdown`) shows each line intact, and the Chinese has no stray spaces.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `18bbe47183ee`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.