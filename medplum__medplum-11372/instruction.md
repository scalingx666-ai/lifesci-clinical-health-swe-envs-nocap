# Issue

**Title:** Match IP access rule prefixes at octet boundaries

## Description

IP access rules currently use unrestricted string-prefix matching, so a rule for `1.2.3.4` also matches `1.2.3.44`. This can unintentionally block valid addresses or allow addresses intended to be blocked by a later rule.

Require an octet boundary when matching partial IPv4 addresses. Complete addresses match exactly; partial prefixes such as `1.2.3` and `8.8.` and the `*` wildcard retain their intended behavior. CIDR support is outside this change.

Add seven regression cases covering allow and block decisions, exact addresses, partial-octet rejection, trailing-dot prefixes, and wildcard matching. Update the IP access rules documentation with the boundary semantics.

Validation:
- All seven focused regression cases pass using a temporary Vitest configuration that preserves the server aliases/setup and skips database global setup. The other 48 tests in the file were skipped.
- ESLint, Prettier, and `git diff --check` pass.
- Server type checking reports two existing missing `isValidCronString` exports in `validation.ts` and `cron.ts`; no errors in changed files.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8c3c4daf609a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.