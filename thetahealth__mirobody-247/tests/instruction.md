# Issue

**Title:** citations: take cited ids as a JSON list, not a comma string

## Description

.

`GET /api/citations` took every id in one `rids` parameter and split it on commas. Two of the three cite kinds can hold a comma: a `ref:doi:` id (the DOI grammar in `agent/knowledge/refs.py` admits any non-space character) and a document cite whose file name has one (`/library/lab results, March.pdf#L12-L14`). The server cut those into pieces that resolved to `unknown`, and no entry came back under the id the client asked about. Percent-encoding does not help, because `query_params` decodes `%2C` before the split.

### Change

| Request | Behaviour |
|---|---|
| `POST /api/citations` `{"session_id": "…", "rids": ["r1", "/library/lab results, March.pdf#L12-L14"]}` | The ids reach `resolve_citations` exactly as cited, with no split and no strip. A body that is not an object with a string `session_id` and a list of strings answers `-1`. |
| `GET /api/citations?session_id=…&rids=r1,r2` | Unchanged. The web client shipped until now sends this. It asks only for row and `ref:` ids, so the only id it still cuts is a DOI with a comma in it. |

The method alone tells the two formats apart, so a single id that holds a comma is never read as a legacy list. As the issue suggests, a body rather than a repeated `?rid=` also keeps file names out of access logs and clear of the URL length limit.

`mirobody/agent/tools/README.md` and `docs/answers.md` now describe the POST.

### Test

`mirobody/tests/test_citation_endpoint.py` covers four cases:

- a POST of `["r1", "/library/lab results, March.pdf#L12-L14", "ref:doi:10.1000/a,b", " r2"]` reaches the resolver unchanged and comes back under the same ids;
- the comma GET still splits;
- malformed bodies are refused;
- the route accepts POST.

Against `main`, the POST case and the route case fail.

```
pytest mirobody/tests/test_citation_endpoint.py -q   → 4 passed
pytest -q                                           → 1266 passed, 121 skipped, 12 xfailed *
ruff check mirobody examples                        → All checks passed
lint-imports                                        → 6 kept, 0 broken
```

\* Run locally without `tests/agent/test_code_tool_probe.py` and `tests/test_code_tool_capability.py`, which need `quickjs_rs`; CI installs it.

### Follow-up

The web client (`thetahealth/mirobody-web`, `resolveCitations` in `src/api/chat.js`) still sends the comma GET. Switching it to the POST is a separate change in that repository, and the `frontend/` build here picks it up on the next sync. That client change has to ship after this one, since an older server answers only GET.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4a641957b738`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.