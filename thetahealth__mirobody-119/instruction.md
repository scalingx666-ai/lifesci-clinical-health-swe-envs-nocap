# Issue

**Title:** Open-source loose ends: quoted genotype rows, build detection test, Docker device setup, °F

## Description

The open items left on the open-source side after #114–#118. Each one was reproduced first, then re-checked after the fix.

## Fixed

**Quoted genotype rows without their header no longer reach a model** (privacy)
- **Was:**
  - MyHeritage and FamilyTreeDNA quote every field (`"rs4477212","1","82154","AA"`).
  - The check for header-stripped genotype rows took quotes off only the ends of a line, so no row matched.
  - Reproduced with the packaged HG00096 samples, quoted as both vendors write them and with the header removed: a chat upload was classed `csv`, and `GeneticHandler.is_genetic_content` returned `False`. So the rows went to document extraction and its model.
  - The packaged samples are unquoted, which is why no test saw this.
- **After:**
  - Quotes inside a row are dropped too, and both shapes are classed `genetic`.
  - The new test fails on the old line (`'csv' != 'genetic'`) and passes on the fix.
  - Ordinary quoted lab tables, and a file with one call row in three, still read as spreadsheets.

**Build detection is tested for the first time**
- The 20-vote / 90 % rule was inline in the loader, and the packaged examples hold 13 sites, so no test ever reached a detected build. It is now `build_from_votes()`.
- Its tests take 25 real catalog sites through `normalize()`, the way the loader counts them:
  - GRCh37 positions → `GRCh37`;
  - GRCh38 positions → `GRCh38`;
  - 13 sites, or a 20/5 mix → `unknown`.

**Device setup on Docker works as the guide says** (`docs/provider-setup.md`, both editions)
- **Was:**
  - The guide told Docker users to edit `config.devices.yaml`. The image carries its own copy of that file, so a credential put there was never read.
  - The verify command `jq '.data[].slug'` fails on the real response, which nests the list under `providers`.
  - "Restart" keeps the old mounts.
- **Now:** put the blocks in `config.localdb.yaml` next to `compose.yaml` and run `./deploy.sh`, which sets `MIROBODY_CONFIG_FILE` and mounts the file. The verify command is `jq '.data.providers[].slug'`.
- **Run on a fresh clone with fake Oura credentials:** `MIROBODY_CONFIG_FILE` was set, the provider loaded, and the new command printed `"theta_oura"`. The old one errored with `Cannot index array with string "slug"`.

**`convert_unit` says why Fahrenheit does not convert**
- °F→°C is refused by design, because conversions here are a single factor. The reply blamed percentages and molar mass.
- It now says temperature scales also differ by an offset, and gives the formula.

## Documented, not fixed

**The OAuth `state` is bound to the account, not to the browser that finishes the link** (the second half of M8)
- SECURITY.md tells operators what that allows and what to do.
- `docs/roadmap.md` has the fix: a `SameSite=Lax` cookie set at link time and checked at the callback.
- It isn't in this PR because it changes every vendor's link flow, and verifying it needs one real authorization per vendor, which nothing here can make.

**AGENTS.md** now says that `test_library_layer.py` and `test_prompts.py` live in the maintainers' gitignored suite, and what a clone can do instead.

## Checks

- **Gates:** ruff 0; compileall; `pytest -q` 240 passed, 13 xfailed; lint-imports 6 kept / 0 broken; the bare import; comment style 0; `phi_lint`, no new findings.
- **Benchmarks:** `benchmarks/genomics` 37 tests OK (2 skipped need external corpora); `benchmarks/health_records` OK.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `13b701a68c5f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.