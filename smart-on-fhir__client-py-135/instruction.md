# Issue

**Title:** Detect oauth2 even if there's no authorize_uri

## Description

As long as we have a JWT and there's a token_uri, we can talk oauth2.

I ran into this while testing the bulk export flow against `https://bulk-data.smarthealthit.org` which does not expose an `authorize_uri`, but does expose `token_uri` and can talk oauth2 with JWTs just fine.

I am not confident that this is the _best_ solution, but it is _a_ solution. Should the code be even dumber and just use oauth2 if the `http://fhir-registry.smarthealthit.org/StructureDefinition/oauth-uris` security extension is present at all? Given that there is no other auth system to fall back to, it seems reasonable to err on the side of oauth2. Happy to tweak this as folks like, or leave it as is.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8e087197f3c9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.