# Issue

**Title:** agent: keep tool-call ids in redacted genotype answers

## Description

`GenotypeRowGuardMiddleware` redacts the answers given after a previous-turn genotype result, and so does `redact_genotype_history` before memory writes. The redaction emptied the answer's `tool_calls` and `invalid_tool_calls` but kept the matching `ToolMessage`s, so the next request carried `tool` messages that answered no call. OpenAI-compatible providers reject that history with HTTP 400 ("Messages with role 'tool' must be a response to a preceding message with 'tool_calls'"). It happens in any conversation where the model called another tool after reading genotype data.

The redacted answer now keeps each call's `id` and `name` and blanks only its arguments, which may hold a copied genotype. Content, `additional_kwargs` and `response_metadata` are still replaced.

This changes a tested contract. Two shipped regressions in `benchmarks/genomics/test_review_regressions.py` asserted `not safe[2].tool_calls`, which is exactly the state that leaves a result answering no call. The second commit makes them check the kept id and name, the empty arguments, and that the redacted result still answers its call. If you would rather drop the orphaned results instead, this PR should change that way.

Verified:
- `python -m unittest discover -s benchmarks/genomics -p 'test_*.py'`: 37 tests OK (2 skipped). The first CI run failed on exactly the two old assertions.
- New local regression (root `tests/`, not shipped): a previous turn with a genotype call, a later tool call that copies the genotype into its arguments, an invalid call and a new question. On 1.5.7 both paths leave `h1`/`h2` unanswered; with the fix none are, and no genotype text remains in the redacted messages. The existing `test_genotype_row_guard.py` still passes (6/6 together).
- Wire check with `langchain-openai` 1.7.2's `_convert_message_to_dict`: on 1.5.7 both paths send orphan `tool` messages `h1` and `h2`; after the fix there are none, and the redacted calls carry `"{}"` arguments.
- Local `tests/agent`: 433 passed, 35 failed, 1 collection error (missing optional deps). The same failure set before and after.
- `ruff check mirobody examples benchmarks/windows` and `scripts/check_comment_style.py mirobody` pass.

CHANGELOG: this branch opens an `## Unreleased` section. Five sibling fix PRs from the same review do the same, so each one merged after the first needs its entry moved into the existing section; no other file conflicts (all six were merged together in a scratch branch).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `21ee06170ab9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.