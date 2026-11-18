# Issue

**Title:** flask demo: don't provide a meaningless default server

## Description

Instead, ask the user to provide the test server. Which is annoying, but...

The flask demo needs an OAuth-capable server, and we are currently using a no-auth server, so the user just sees a message "nothing to demo here".

This is because:
- The old (oauth) server that presumably worked was taken down.
- We put in the new (non-oauth) R4 modern test server.
- The modern server has a temporary bug where its metadata doesn't validate
- So we didn't notice that the flask server wouldn't work even if validation passed.

All of the [public test servers](https://confluence.hl7.org/display/FHIR/Public+Test+Servers) I know about require you to email someone to set up a user. So it's not obvious what a good replacement would be.

Honestly, we should probably just add a new default demo that supports no-auth servers and still shows something interesting.

But for now, this gets the flask demo to a more honest place and asks the user to provide their own server. :shrug:

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `34b0ddc4ca65`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.