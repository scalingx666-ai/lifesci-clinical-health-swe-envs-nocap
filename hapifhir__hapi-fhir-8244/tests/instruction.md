# Issue

**Title:** Fix for $meta-add and $meta-delete operations within transaction bundles

## Description

### Root Cause

RuleImplOp.applyRuleToTransaction parsed each entry's request.url with UrlUtil.parseUrl(...) to derive the target resource for rule evaluation. For Patient/p1/$meta-add, the trailing $meta-add segment isn't a resource id or _history, so parseUrl threw HAPI-1742 — before the transaction processor (which already supports these operations, #7734) was ever reached.

### Changes:

- RuleImplOp: detect an operation URL (trailing segment starting with $) and parse only the ResourceType/id prefix, so authorization resolves against Patient/p1.
- Added isMetaOperation(...) and exempted $meta-add / $meta-delete from the nested-Parameters guard (Msg.code(339)), since these legitimately carry a Parameters body via POST.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e6b012ee158a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.