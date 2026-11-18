# Issue

**Title:** FHIR-57725: Note multiple-morphology demonstration in Skin Patch example description

## Description

Resolves [FHIR-57725](https://jira.hl7.org/browse/FHIR-57725): Example missing from morphology ticket (Technical Correction, follow-on to FHIR-56262)

## What changed
The Skin Patch BodyStructure example (`bodystructure-example-skin-patch`) already demonstrates recording **multiple morphology codes at a single included structure** — the example requested in FHIR-56262 (codes `275265005` Basal cell carcinoma and `707136009` Nevus sebaceous). However, its entry in `list-BodyStructure-examples.xml` described it only as a clinical-trial skin-patch example, so the multiple-morphology demonstration was **not discoverable** on `bodystructure-examples.html`.

This extends that example's description to call out the multiple-morphology demonstration, so it appears in the examples list:

> …subject to repeated observations and/or procedures over time**. It also illustrates recording multiple morphology codes (basal cell carcinoma and nevus sebaceus) at a single included structure**

No new example resource is created and the example content is unchanged — this is a description-only correction.

## Files touched
- `source/bodystructure/list-BodyStructure-examples.xml`

## Notes
- Non-substantive (Change Impact: Non-substantive). Per WG decision, the existing `707136009` "Nevus sebaceous (disorder)" code is retained as the equivalent of the ticket-named `29783009`.
- Local FHIR-Core publisher builds in this environment rewrite `structuredefinition-BodyStructure.xml`'s `contentReference` into an unresolvable absolute form (failing the build independent of this change); CI builds from the clean checkout, where `origin/master` carries the resolvable `#BodyStructure.includedStructure` form.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `192ac53681c0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.