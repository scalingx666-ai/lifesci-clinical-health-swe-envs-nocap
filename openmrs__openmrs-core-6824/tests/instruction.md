# Issue

**Title:** Remove the stray ">" after the root element of infinispan-api-local.xml

## Description

## Problem

`api/src/main/resources/infinispan-api-local.xml` ends its root element with a doubled `>>`:

```
<infinispan ... xmlns="urn:infinispan:config:15.2">>
```

It has been there since the file was introduced (8f3dfa5cf, TRUNK-6302 / #5027).

## Impact

None functional - the characters after the start tag parse as text content, so Infinispan accepts the file and everything works today. But the malformed root tag is flagged by XML linters, IDEs and schema-validating tooling, and it is an easy-to-miss trap for future edits of this file.

## How this fixes it

Drops one `>` so the root element ends normally. A 1-file, 2-character change, no other edits.

## Related

Spotted while working on TRUNK-6415 / #6605; per review it is being fixed in its own PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d30e99ee3d93`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.