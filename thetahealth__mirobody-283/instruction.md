# Issue

**Title:** release: 1.6.1

## Description

Cuts 1.6.1. **Merge #265 and #282 first** (this branch sits on both), as merge commits; this PR's own diff is then the release commit alone. Please merge nothing else into main until the tag: every check below ran on this exact tree.

## What ships

Since 1.6.0 (#264), main has #267, #273, #272, #274, #276, #269, #270, #278, #279 and #280, and #265 and #282 go with it. CHANGELOG has each one under 1.6.1. In short:

- A series printed in two units is answered in one: the web chart, stats, trend and the model all read the same unit (#271, #272).
- `query_health_indicators` names each series once. The printed name and the printed number stay out of the model's context. Computed numbers are written to six significant figures. A device metric reads as its name, not its key (#277, #278).
- A result that mixes series states each series' constants once, and only where that is shorter (#269). Series without a LOINC display are named in every view (#270).
- An upload made while a local model is still loading says so, in the page's language, instead of 已处理 with no readings (#275, #276). code_exec says why there is nothing to compute (#274).
- The journal names a coded reading in the reader's language (#265).
- A deleted upload stays deleted, a file reads 处理中 until its readings are in, and 重新处理 reads a file again (#279). A scanner's settings and a history heading are no reading (#280, part of #235).
- A reinstalled stack (`down -v`, same `.env`) neither locks out its first account nor lets an old browser token into it (#282, found while testing this release).

**Upgrade notes** (in the CHANGELOG): nothing to migrate or re-import. Run `git pull` and `./deploy.sh` with the same `COMPOSE_PROFILES`, which pulls `thetahealth4mirobody/mirobody:1.6.1`. There are two schema changes, both made at the first start: the `th_upload` table and a `tokens_valid_after` default for new accounts. A file 1.6.0 left 已处理 with no readings is not read again on upgrade: choose 重新处理 on it once the model is ready.

The Apple import path is unchanged since 1.6.0. Two paths in this release delete data: deleting an upload in flight, and reprocessing, which erases a file's readings first. Both were exercised below.

## The release commit

- The six version strings in the four files `check_versions` reads are now 1.6.1. Unreleased becomes 1.6.1, and an empty Unreleased stays on top.
- Test counts in `docs/testing.md` and `AGENTS.md` are re-measured in fresh venvs on a clone-shaped tree:

  | install | packages | tests |
  | --- | --- | --- |
  | `[test]` | 20 | 841 passed, 269 skipped, 12 xfailed |
  | `[test,parse]` | 76 | 939 passed, 260 skipped, 12 xfailed |
  | `[test,app]` | 147 | 1230 passed, 169 skipped, 12 xfailed |

  Plain `pytest -q` with `[app]` collects 1681 tests: 1500 passed, 169 skipped, 12 xfailed. All 169 skips are database cases (157 Postgres regressions, 12 Apple transport election). The suite has 47 public modules. The per-extra breakdown is recomputed from per-module junit diffs.
- `frontend/` is unchanged: main's bundle is built from mirobody-web `199e9e4`, whose tree is web main's (`efc0567`).

## Verified

Everything below ran on this branch's tree, or on an image built from it (`docker build --build-arg MIROBODY_VERSION=1.6.1`).

- **Gates:** ruff, compileall, comment style, PHI lint, `check_versions` and `lint-imports` (6 kept, 0 broken) are clean, and the bare library layer imports. Full suite against PostgreSQL 17: 1681 collected, 0 failed.
- **e2e, all six stages** (upload, extract, indicators, verify, units, chat; cloud key via OpenRouter): **PASSED, 245 readings**. 1.6.0's release run had 254. Per file:
  - `zhangshu_pdf` 118 → 114: the four rows are the ultrasound scanner settings #280 drops. None of `AO% D DR FR Frd Frq Gn PAT TIS S/A` is stored; the ECG's `RV5` and `SV1` are kept.
  - `wx_250_jpg` (FibroScan photo) 9 → 3: stiffness 8.1 kPa, CAP 247 dB/m and the success rate are kept. The dropped rows are quality statistics, which follow OCR text length (832 characters then, ~640 now, the same drop as 1.6.0's own rerun).
  - `hengxiang_jpg` 8 → 5: the narrative is split into organ findings differently.
- **Upgrade from 1.6.0, the user's path:** a stack on the 1.6.0 tag (its compose file and the `1.6.0` image), with a local model router stuck loading.
  - It reproduced #275 exactly: at +300 s the file read 已处理 with 0 readings and no reason (its rule reader stored 9 at +892 s).
  - Then `git checkout` to this branch and `./deploy.sh`: all 14 schema files ran, `th_upload` exists, the default is set, the 3 existing accounts keep `tokens_valid_after` NULL, and the 9 readings are intact.
- **#275 on this image:** an upload while the model loads fails at 120 s with "本地模型 minicpm5-2b 还在下载或加载中，等设置页显示就绪后再重新上传". Once the model was ready, **重新处理** on that row gave the 9 readings, and 指标 listed them with LOINC codes.
- **The two paths that delete data:**
  - Reprocessing a complete file: 9 → 9 readings, 9 distinct fingerprints, identical values.
  - Deleting a file while it reads 处理中: the row is soft-deleted, the stored object is removed and the cascade runs. The extraction that ends afterwards writes nothing (`file not found for update`), and the readings count is unchanged.
- **Reinstall (`down -v`, same `.env`), #282:** a token from before is refused (401) both before and after the new account takes its id 3. The new account's own token answers 200, and the browser signs in straight away.
- **#271 on the local model** (MiniCPM5-2B on a llama.cpp b11429 router; on a Mac the router runs on the host): the units stage PASSED. Asked whether total cholesterol went up or down, it answers "5.48 → 4.90 mmol/L，下降了 0.58" and LDL "3.57 → 3.10". The chart draws one unit with 212 mg/dL shown as printed.
- **Wheel and sdist:** `check_wheel_data` finds all 33 data files, and `twine check` passes. In a clean venv outside the repo the wheel installs 2 packages, reports 1.6.1, resolves 血红蛋白 → 718-7, and `mirobody mcp` lists 6 tools.

Not covered: the Apple import (unchanged since 1.6.0) and the in-container `local-cpu` profile. This machine's Docker VM has 5.8 GiB, below the 8 GB the README asks for, so the same models ran on host routers.

## After merge

Tag `1.6.1` on this PR's merge commit. The release workflow publishes PyPI, the MCP Registry and the Docker image `1.6.1` + `latest`. Then check all four channels, and pin the docs site to the tag.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0d9c88c43e89`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.