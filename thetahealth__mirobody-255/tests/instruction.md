# Issue

**Title:** frontend: load the entry chunk the 985f3c2 sync renamed

## Description

## What was wrong

On `main` at c4a9d4be every page of the web client is blank. #254 (42fc16c9) synced `frontend/` from thetahealth/mirobody-web 985f3c2 but committed only `assets/`: `frontend/index.html` still loads `/assets/index-mKXkiuxp.js`, which the same sync renamed to `index-BeE5V1R2.js`. The entry script 404s and React never mounts. No release carried it.

## What changed

- **`frontend/index.html`** is now the one the 985f3c2 build writes. I rebuilt `build:opensource` from a clean clone at 985f3c2: all 70 files in `dist/assets/` match `frontend/assets/` byte for byte, and its `index.html` differed from main's only in the script src. The modulepreload (`vendor-antd-DpKwsjII.js`) and stylesheet (`index-IbnKvKED.css`) lines were already right. After this change `diff -rq dist/ frontend/` is empty.
- **`mirobody/tests/test_frontend_bundle.py`**, a new gate. It parses `index.html`, then follows every chunk it loads, using the three spellings Vite writes (`/assets/x`, `assets/x` in `__vite__mapDeps`, `"./x"` sibling imports). It fails on any file `frontend/` does not hold. On this tree the walk reaches all 70 assets plus the icon. On main's `index.html` it fails with `index.html -> assets/index-mKXkiuxp.js`. Two synthetic cases pin the 985f3c2 shape and each reference spelling, so the gate cannot pass because its patterns stopped matching. It skips where there is no `frontend/` (an installed wheel). It needs only the stdlib, so it runs in both CI pytest steps.
- **`docs/frontend.md`**: "Replacing the client" now says to commit `index.html` with the chunks and to run the gate.
- **CHANGELOG** "Unreleased → Fixed": an entry under the 985f3c2 entries.

## Browser check

I started an isolated stack (`docker compose -p fefix`, port 18960) from a local image built from `main` at c4a9d4be. Its `frontend/assets/` matches this branch by sha256. I set `LOCAL_BASE_URL` to an unused address so `/login` does not redirect to first-run setup. No key was involved.

| | `index.html` | `/login?lang=en` | Network log |
|---|---|---|---|
| Before (image as built from main) | names `index-mKXkiuxp.js` | blank, `#root` empty | `GET /assets/index-mKXkiuxp.js → 404` |
| After (`docker cp` of this branch's `index.html`, `cmp` identical) | names `index-BeE5V1R2.js` | login form renders: logo, demo-account hint, Sign in / Create account / Email code | 14 requests, all 200 (entry, antd vendor, CSS, AuthShell, LanguageSwitch, `/mirobody.json`, wordmark, font). No 404, no console errors |

## Gates

- `pytest -q`: 1283 passed, 122 skipped, 12 xfailed. Two files did not collect locally (`tests/agent/test_code_tool_probe.py`, `tests/test_code_tool_capability.py`) because this venv has no `quickjs_rs`. That predates this change.
- `ruff check mirobody examples benchmarks/windows`: clean
- `python -m compileall -q mirobody`: clean
- `lint-imports`: 6 kept, 0 broken
- Library layer import, comment-style gate and PHI log gate: clean

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c4a9d4be2f0d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.