# Issue

**Title:** docs: list the MCP directories and the DeepSeek Harness plugin

## Description

## What was wrong

1.6.0 is in the official MCP Registry as `ai.thetahealth/mirobody`, and directories that mirror the registry list it. Two of them describe it from our own text, and that text left room for mistakes:

- **AddonAudit** ([listing](https://addonaudit.com/addon/ai-thetahealth-mirobody/)) runs the stdio server in a sandbox: handshake, six tools, no advisories, score 100, tier "Audited". It could not tell whether `normalize_unit` and `convert_unit` run offline, because their descriptions did not say so.
- **mcprush** ([listing](https://mcprush.com/thetahealth/mirobody-mcp)) gives `uvx 'mirobody[agent]' mcp` as the install line, about 93 packages instead of 2. `examples/README.md` was the only page pairing that extra with MCP.

The READMEs named neither the registry entry nor the community DeepSeek Harness plugin, [zwbao/dsh-plugin-mirobody](https://github.com/zwbao/dsh-plugin-mirobody).

## What changed

- `mirobody/mcp/stdio.py`: `normalize_unit` and `convert_unit` say "offline", like the other terminology tools. Descriptions only; no schema changed.
- `examples/README.md`: the row for example 04 says `[agent]` is for the MCP SDK the script loads, and that `mirobody mcp` needs only `pip install mirobody`.
- `README.md`, `README.zh-CN.md`, `README.ja.md`, all three editions:
  - "Build on Mirobody" gains a row for the DeepSeek Harness plugin.
  - A short paragraph names the registry entry and two directories that list it, and says to take the install line from the README, since each directory syncs on its own schedule.
- `glama.json` (new, repository root) names `saltyfishtree` as maintainer. awesome-mcp-servers merges a server only after Glama has listed and checked it, and Glama has no Mirobody entry. For a repository owned by an organization, Glama's claim flow reads its maintainers from this file ([Glama's description](https://glama.ai/blog/2025-07-08-what-is-glamajson)).
- `CHANGELOG.md`: an Unreleased entry.

The plugin's 0.1.3 record-tool parameters match 1.6.0's schemas: `query_health_indicators` (`keywords`, `indicators`, and the nine `view` values), `query_medications`, `query_genetic_data` and `query_pharmacogenomics`. I checked them against the schemas the server loads.

## Checked

- `ruff check mirobody examples`, `compileall`, `lint-imports` (6 kept, 0 broken).
- `pytest -q`: 1460 passed, 150 skipped, 12 xfailed.
- `mirobody mcp` over stdio, `tools/list`: five of the six tools say "offline". `standardize_report` does not, because it calls a model.
- The maintainers' README, examples, doc-path and MCP tests: identical results on this branch and on unchanged `main`.

thetahealth/mirobody#265 also adds an Unreleased entry, so whichever of the two merges second has a one-line `CHANGELOG.md` conflict.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5681e7176dce`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.