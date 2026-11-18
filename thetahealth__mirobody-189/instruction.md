# Issue

**Title:** mcp: publish the registry entry, validate it on every PR

## Description

## Why

`server.json` has shipped since 1.5.1 but was never published. The official MCP Registry has no Mirobody entry, so neither do the GitHub and VS Code lists that read from it. Meanwhile mcp.so, mcp.directory and TypingMind still list a retired **Theta Health MCP**, and its repository (`theta4ai/theta-health-mcp`) now returns 404.

## What changes

- **Name stays `ai.thetahealth/mirobody`.** It matches the repository and the PyPI author, and the PyPI README of 1.5.8 already carries it, so **1.5.8 can be published right after merge**. Registry names are permanent, so this settles it before the first publish.
- **Description** names what the tools code to, checked by running them: *Lab results to LOINC codes and UCUM units, symptoms and diagnoses to ICPC-3. Offline, no API key.* FHIR is only the Observation the codes come back in.
- **Every PR** runs the registry's own `mcp-publisher validate` on `server.json` and checks that README.md carries the matching `mcp-name` (job `mcp-entry` in test-build.yml; it passed on this PR).
- **New workflow `mcp-registry.yml`**: `pypi-release.yml` calls it after the PyPI check, and it can also be dispatched by hand. It reads `server.json` from the ref the run is on, checks that `tag` equals its version, validates, signs in as thetahealth.ai, publishes, then asks the registry for that version. A missing key fails the run by name.

## Needs the owner (one time)

1. Run the `openssl` commands in the workflow header. Add the printed `v=MCPv1; k=ed25519; p=…` line as a **TXT record at the thetahealth.ai apex** (Route 53). The existing apex TXT records stay as they are.
2. Create the **`mcp-registry` environment**, restricted to `main` and release tags, and add the secret **`MCP_REGISTRY_KEY`**.
3. Run *Actions → MCP Registry → Run workflow* on `main` with `check_only` ticked. A green run means the TXT record and the key match.
4. Run it again on `main` with tag `1.5.8`, `check_only` unticked. That publishes the entry. From then on, each release publishes its own version.

## Outside this repo (not done here)

- mcp.so and mcp.directory: submit Mirobody, and ask them to retire the `theta-health-mcp` listing.
- mcpmarket.com: its Mirobody entry still shows the pre-1.2 description and 1,034 stars.
- npm: `npm deprecate theta_health_mcp "Retired; use Mirobody: uvx mirobody mcp"`, run by the package maintainer.
- thetahealth.ai: `/mcp` and `llms.txt` still describe the old MCP.

## Verified

- `server.json` validates against the 2025-12-11 schema and with `mcp-publisher validate` in CI.
- `check_versions`, actionlint, ruff, compileall and lint-imports (6 kept) pass.
- pytest: 1096 passed, 111 skipped, 12 xfailed.
- `uvx --python 3.12 mirobody==1.5.8 mcp`, run from outside the repo with no key, completes the MCP handshake and lists 6 tools. 总胆固醇 5.2 mmol/L → 14647-2 (UCUM mmol/L), 头疼 → ICPC-3 NS01, 高血压 → KD73.
- The publish itself is unverified until the key exists.

The branch renamed the entry to `ai.mirobody/` and then back, so please **squash-merge**.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `18bbe47183ee`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.