# Issue

**Title:** llm: an empty completion is no answer, not an AttributeError

## Description

The OpenAI client returns `None`, without raising, when an endpoint answers HTTP 200 with a JSON `null` body — measured against a local server on openai 3.28, also with leading blank lines before the `null`; a 503 raises `InternalServerError` instead. On 1.5.10 a 587 s `deepseek-utils` call ended that way during the provider's 503 outage, and `async_get_structured_output` dereferenced it:

```python
result = response.choices[0].message.to_dict()   # AttributeError: 'NoneType' object has no attribute 'choices'
```

The broad `except Exception` below turned that into `structured output failed: … error_type=AttributeError` — a log that names a line in this repo instead of the model that sent nothing. Reported from a live deployment on 1.5.10 (#239).

The same unguarded access was on the other two OpenAI-compatible surfaces, so all three are covered:

| Surface | Contract | On an empty 200 |
|---|---|---|
| `async_get_structured_output` | `None` = no model answered | returns `None`, logs `structured output: no response: model=…` |
| `async_get_text_completion` | `None` = no model answered | returns `None`, logs `text completion: no response: model=…` |
| vision `image_extract` | a failed request raises | raises `NoResponse`; `failure_reason` passes its message to the uploader instead of the bare type name |

The native Anthropic path streams (`messages.stream` → `get_final_message()`); a null body there raises from the SDK's stream helper, which the existing handlers already treat as a failed call, so it is unchanged.

**What does not change:** callers still see a failed extraction; this is a diagnosis fix. The upload a vision failure ends now reads "`<model>` sent back an empty response, which an overloaded provider does; try again later, or point the route at another model."

### Test

`mirobody/tests/test_llm_no_response.py` fakes a client whose `create` returns `None` and covers each surface: return value **and** log for the two text surfaces (the broad handler would return `None` anyway, so the log is what proves the guard), `NoResponse` for vision, and the uploader's message. Removing the text and vision guards fails two of the four.

```
pytest mirobody/tests/test_llm_no_response.py -q   → 4 passed
pytest -q (whole tree)                              → 1266 passed, 121 skipped, 12 xfailed *
ruff check mirobody examples                        → All checks passed
lint-imports                                        → 6 kept, 0 broken
```

\* run locally without `tests/agent/test_code_tool_probe.py` and `tests/test_code_tool_capability.py`, which need `quickjs_rs` and the local venv predates it; CI installs it.

Thanks to @yuyun2000 for the log forensics that isolated this from the provider outage.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e7caaafd9aba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.