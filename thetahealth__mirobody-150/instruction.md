# Issue

**Title:** Align hosted and local demo facts with a deterministic export contract

## Description

The hosted walkthrough used a separate sample story, so its people, readings
and source files could differ from the self-hosted demo. Add a deterministic
JSON exporter over the existing seed and upload panels, including the view-only
family grant, collection dates and source-file hashes. Upload samples remain
outside the initial record, and exporting needs no database, model or deployment
configuration.

Both READMEs expose Global and China demo links. The English README and demo
guide request English in both regions; the Chinese README requests Simplified
Chinese in both regions. Region and page language are independent. Remove
obsolete hosted developer-API recommendations from the READMEs and guides.
The local demo accounts and codes remain local-demo configuration.

Validation: 10 hosted entry links match their document language; the English
README's three demo GIFs were inspected at the start, midpoint and end. Three
public export-contract tests pass; source pytest: 620 passed, 99 skipped,
12 expected failures; ruff over the engine and examples; compileall; six import
contracts kept; library imports verified against this checkout. The existing
demo/generate.py has two lint findings when linting the entire demo directory;
it is unchanged.

The matching cloud correction adds a permanently visible language switch at
the top of /demo, honors URL language before stored preferences, and preserves
the choice through sign-in and refresh. Cloud frontend validation: 859 tests,
lint, both regional builds, plus desktop/mobile checks in both languages.

The hosted demo keeps the application's Data / Indicators / Ask navigation on
both desktop and mobile, using the same navigation definition as the signed-in
client. Trial and self-host entry actions each appear once in the header;
regional recommendations appear after a sample task completes. Member switching,
the record and indicator views, report sources and the chat input retain the
application's structure.

Review the matching hosted changes on testing:

- [Global demo in English](https://test-chat.mirobody.ai/demo?ref=github-readme&lang=en)
- [China-hosted demo in English](https://test-chat.mirobody.cn/demo?ref=github-readme&lang=en)
- [Global demo in Simplified Chinese](https://test-chat.mirobody.ai/demo?ref=github-readme&lang=zh-cn)
- [China demo in Simplified Chinese](https://test-chat.mirobody.cn/demo?ref=github-readme&lang=zh-cn)

The README links keep their production hosts. Release the matching hosted
walkthrough and language correction to production before merging the entry-link
changes. This PR remains for maintainer review; no merge or production release
is performed by this change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f4fcee681b3a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.