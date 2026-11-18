# Issue

**Title:** personal MCP links: document one URL per record; activation revokes too

## Description

#232 asked two things about personal MCP links for a managed family member: is minting one supported, and what happens to it when access changes or the member takes the account over. The mechanism was only ever described in the CHANGELOG (1.5.3, security section), so `docs/answers.md` — the page that says "no parameter names a person" — gave no way to learn it. Checking the answer against the code turned up one path where it was not true, so this PR fixes that path as well as documenting it.

### Docs

One paragraph in `docs/answers.md`:

- a link is bound to the pair (creator, subject), so managing two people means two links and two MCP server entries;
- `POST /personal/mcp` with `{"user_id": …}` is authorised through the care circle;
- it lives 10 days from when it is made, not extended by use (`MCP_URL_TTL_DAYS`);
- stopping the share, leaving the circle, or the member taking the account over and choosing not to share revokes it, and sharing again does not revive the old URL; deleting either account ends it at once.

### Fix: activation that shares nothing now revokes

`activation.hand_over` wrote the new owner's `health_access` straight into `care_circle_members` and skipped the revocation that `set_health_access` and `remove_member` run. Choosing "none" at activation left the creator's link refused but live, and raising the switch later — within the link's 10 days — made the old URL read the record again. `hand_over` now calls the same revocation after it writes the membership. It only revokes what the circle no longer allows, so a choice that still shares changes nothing. `care_circle._end_links` becomes `end_links`, since a module outside `care_circle` now writes memberships too.

### Test

New PostgreSQL regression in `mirobody/tests/test_postgres_regressions.py`: mint a link for a managed member, hand the account over with "none", then raise the switch. The link stays refused and its row reads `revoked_by = 'care_circle'`. Without the call the test fails on the revocation. The fixture now also loads `62_personal_mcp.sql`.

```
pytest mirobody/tests/test_postgres_regressions.py (PostgreSQL 17)  → 122 passed
pytest -q (whole tree)                                               → 1262 passed, 122 skipped, 12 xfailed *
ruff check mirobody examples                                         → All checks passed
lint-imports                                                         → 6 kept, 0 broken
```

\* run locally without `tests/agent/test_code_tool_probe.py` and `tests/test_code_tool_capability.py`, which need `quickjs_rs` and the local venv predates it; CI installs it.

The member picker in Settings is a client change, in `thetahealth/mirobody-web`, and is not part of this PR.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8cdb1430abe6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.