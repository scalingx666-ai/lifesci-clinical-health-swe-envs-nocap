# Issue

**Title:** accounts: a reinstall's first account takes no old token

## Description

## What was wrong

A stack started again on a new database (`docker compose down -v`, then `./deploy.sh`) keeps `.env`, and so its JWT key, and numbers accounts from 1 again. A browser still holding a token from before hits one of two outcomes:

- **It asks before anyone signs up.** `is_active_account` finds no row and adds the id to `_closed` for the life of the process. The next person to sign up gets that id and every token they receive is refused. Sign-up answers ok, the page goes back to the sign-in form, and the console shows a 401. Found while testing 1.6.1 on a reinstalled local stack (1.6.0 image, user id 3).
- **It asks after someone signed up.** The old token opens the new account, because `tokens_valid_after` was NULL, so a token minted at any time passed.

## What changed

Both halves are needed. Either one alone leaves the other outcome in place.

- `mirobody/user/user.py`: a lookup that finds no account is no longer remembered. An account closed through `close_account` is still remembered for good.
- `mirobody/schema/10_accounts.sql`: `tokens_valid_after` defaults to the account's creation time less one minute. The minute is the same `ISSUED_AT_SKEW` that `iat` already allows for clock skew, so the first token, minted right after the insert, still passes when the database's clock runs ahead. Every insert into `health_app_user` (sign-up, code sign-in, managed members, demo seed) gets the default. `ALTER ... SET DEFAULT` leaves existing rows as they are.

## How to tell

With the old page open, run `docker compose down -v` and `./deploy.sh`, then sign up. The data page opens, and the old page's token is refused.

## Tests

- `test_security_gates.py::test_a_token_for_an_account_not_there_yet_does_not_shut_it_out`: the lookup miss. Fails on main.
- `test_postgres_regressions.py::test_a_new_account_refuses_a_token_minted_before_it_existed`: both halves against PostgreSQL. Fails on main, and also fails with only the `user.py` change.
- Full suite with `MIROBODY_TEST_POSTGRES_DSN` (PostgreSQL 17): 1665 passed, 12 xfailed. ruff, compileall, comment style, PHI lint and `lint-imports` (6 kept, 0 broken) are all clean.

Intended for 1.6.1.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0d9c88c43e89`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.