# Issue

**Title:** Render OpenAPI Markdown with commonmark instead of flexmark

## Description

`OpenApiInterceptor` is HAPI's only flexmark user, and FHIR core already brings `org.commonmark:commonmark`. Switching drops flexmark from `hapi-fhir-server-openapi`. The root now manages `org.commonmark:commonmark` at 0.21.0 (FHIR core's version), and the unused `com.atlassian.commonmark` 0.9.0 entry is gone.

**For review**
- `OpenApiInterceptorMarkdownTest` pins flexmark's output for 47 inputs. Two change:
  - `[a](<http://x.com/a b>)` now renders as a link; current CommonMark allows spaces inside `<…>`.
  - `JavaScript:` links are now suppressed too. The `javascript:` suppression flexmark had is reproduced, and is now case-insensitive.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8d07589c2cdc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.