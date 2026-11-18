# Issue

**Title:** Treat RDF/Turtle as an unsupported format when Apache Jena is not on the classpath

## Description

Jena is optional in `hapi-fhir-base`, but without it a Turtle request (`_format=ttl`, `Accept: text/turtle`, a Turtle body, or RDF as the default encoding) fails with `NoClassDefFoundError` and a 500. Now Turtle is treated like any other format the server can't produce or read. With Jena present, nothing changes.

**For review**
- Without Jena:
  - `_format` and `Accept` fall back exactly as they do for an unknown format.
  - A Turtle body gets a 400 (HAPI-3062), mirroring HAPI-0449.
  - A default encoding of RDF serves JSON, with one warning at startup.
- A `Binary` posted as `text/turtle` without Jena is stored as raw content, as for any non-FHIR type.
- `Msg.code(3062)` needs an entry in the error-code wiki table.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8d07589c2cdc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.