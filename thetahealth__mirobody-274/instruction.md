# Issue

**Title:** code_exec: say why there is nothing to compute on

## Description

## The problem

`code_exec` computes only on what a record tool returned **in this turn**. In a follow-up ("画个图看看", "算一下这三次的平均值"), a model sends the numbers from the previous turn instead. The tool refuses, correctly, but by raising `ValueError("Call a record tool before computing…")`.

`ToolFaultMiddleware` never passes an exception's message to the model (a driver's message can quote SQL with bound values). So the model reads:

```
{"error": "code_exec failed (invalid_arguments)", "hint": "Check the tool's parameter list and try once with corrected arguments."}
```

It concludes its arguments were wrong ("The code_exec tool only takes a `code` parameter…") and resends the same call. Found while testing #272 in chat on a local stack with MiniCPM5-2B.

## The fix

The three refusals in `source_results` become `NoSource`, still a `ValueError`, so existing callers and tests hold:
- nothing looked up in this turn;
- the lookup failed;
- the lookup returned no rows.

Both engines catch `NoSource` and return a recoverable error result carrying the reason, the way the "executor unavailable" path already did. The first refusal now says to call the record tool again, and that charting readings already in the conversation needs no `code_exec`.

## Checked

| MiniCPM5-2B, same DB, "算一下这三次的平均值，用代码算" after a cholesterol lookup | `code_exec` calls | Answer |
|---|---|---|
| Before | 4, each "check the tool's parameter list"; the last was `5.48 + 4.6 + 4.90 / 3` | "平均值计算如下：" and no number |
| After (two runs, identical) | refused once with the reason → `query_health_indicators` → computed | 4.994 mmol/L (correct) |

- New `mirobody/tests/test_code_exec_says_why.py`: 3 tests, red on `main`, green here.
- The maintainers' code-tool suite: 43 passed.
- ruff, the comment-style gate, `lint-imports` 6/0 and the PHI gate pass; the suite without a DSN passed.

Independent of #272: it touches only `mirobody/agent/code_tool.py`. A `1.6.0-fix.2` test image carries both.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b7a3ba69d5b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.