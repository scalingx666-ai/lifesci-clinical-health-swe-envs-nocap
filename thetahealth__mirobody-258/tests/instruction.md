# Issue

**Title:** account merge: move a family member's MCP link to the kept account

## Description

#232 follow-up. The reply there says that when a managed member takes their account over and keeps sharing, the creator's personal MCP link keeps working and shows up in the member's own list of links. That holds when the managed account simply becomes theirs. It did not hold when they take it over by signing in to an account they already had: activation then merges the two, and `account_merge` did not touch `th_personal_mcp_url`.

### What was wrong

After the merge the creator's link still named the closed account, so:

- `authorize` refused it even when the person chose "view", because `resolve_subject` joins both accounts on `is_del = false`;
- it stayed listed as live in the creator's "links I made" until it expired;
- it was missing from the person's "links that read my record", the list where they would revoke it.

It failed closed, so nothing leaked, but it broke the promise in the issue and left a dead row on screen. Binding an address that belongs to another account (`reason="email_link"`) goes through the same merge and had the same gap.

### Change

A new conflict-aware step, `_merge_personal_mcp_links` in `mirobody/user/account_merge.py`, runs inside the merge transaction:

1. Unrevoked links that read the closed account move to the kept one. Every use is still checked against the care circle. An activation that chooses "none" then revokes the link through `end_links` (#243), the same as without a merge.
2. Links the closed account made, and the kept account's links to the closed one (which would become a second link to its own record), are revoked with `revoked_by = 'account_merge'`. They stay on the closed account as history.
3. If one creator holds unrevoked links to both records, the one that expires later is kept. Expired rows count, because `uq_th_personal_mcp_url_live` covers every unrevoked row; without this step the move would violate it.

Docs: a sentence in `docs/answers.md`, a bullet in the `personal_mcp` module docstring (which also stops saying only `care_circle` revokes), and a CHANGELOG entry under Unreleased.

### Tests

Three new PostgreSQL regressions in `mirobody/tests/test_postgres_regressions.py`:

- `test_activation_into_an_existing_account_carries_the_creators_link[view]`: the link reads the kept account and appears in both lists.
- `test_activation_into_an_existing_account_carries_the_creators_link[none]`: the link is revoked by `care_circle`, and raising the switch later leaves it refused.
- `test_account_merge_keeps_one_unrevoked_link_per_creator_and_record`: one case covers rules 1–3, including an expired, unrevoked collision.

All three fail on `main` without the change (`'3' == '4'` twice, then `KeyError: 'th_personal_mcp_url'`) and pass with it.

```
pytest -q (whole tree, MIROBODY_TEST_POSTGRES_DSN on PostgreSQL 17)  → 1448 passed, 12 xfailed *
ruff check mirobody examples                                         → All checks passed
python -m compileall -q mirobody                                     → ok
lint-imports                                                         → 6 kept, 0 broken
python3 -c "import mirobody.kernel.meds, mirobody.kernel.query"      → ok
```

\* run locally without `tests/agent/test_code_tool_probe.py` and `tests/test_code_tool_capability.py`, which need `quickjs_rs`; the local venv predates it, and CI installs it.

#232 stays open after this merges: the member picker in Settings is thetahealth/mirobody-web#23 plus the `frontend/` sync in #257.

### Local end-to-end test (#257 and #258 together)

One image built from #258 with #257 merged in, on an isolated Docker Compose stack, driven through the web client. Every link was called with the official MCP Python SDK and checked against `th_personal_mcp_url`.

| Case | Result |
|---|---|
| Settings → MCP link: rows for self, an invited member and four managed members; six links minted | each link read only its own person's record |
| Activation to a new address, "none" | 401, `revoked_by = care_circle`; sharing again later leaves it 401 |
| Activation to a new address, "view" | 200; listed under "who holds my link" in that person's Settings |
| Activation into an account that already existed, "none" | link moved to the kept account, then 401, `revoked_by = care_circle` |
| Activation into an account that already existed, "view" | 200 on the merged record; listed in that person's own Settings |
| Creator held links to both merged records | the one expiring later kept; the other 401, `revoked_by = account_merge` |
| Revoke from Settings | 401 |

Afterwards no row in `th_personal_mcp_url` named a closed account.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b65c0b83a195`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.