# Issue

**Title:** chat: attach citations to stated numbers; fix calculation input transfer; expose unit conversion

## Description

## What this does

**A citation is a claim about provenance, and the turn already has the evidence.** A chat
turn holds every row the record tools returned, so `<cite>[rN]</cite>` no longer depends on
the model remembering to type it: a number in the answer is matched against those rows
(value within tolerance) and cited right after its unit - `69.5 kg<cite>[r3]</cite>`.

**The numbers no row supports are the review signal.** A figure the answer states that the
record does not contain is left uncited *and* returned on the text block as `auto_uncited`,
so a UI or an auditor can show it beside the cited ones; a count alone would hide which
figure to check. `AUTO_CITE=off` keeps the previous behaviour.

**A calculation could fail before it ran.** The sandbox uploaded `data.json`, `main.py`
and `runner.py` through `docker exec` with an attached stdin. With some docker
SDK/daemon pairs that call returns no exit code and the payload is dropped, so every
calculation answered *"calculation inputs could not be transferred"* while the query and
the tool were fine. The files are now written with a base64 body over an ordinary shell
command, which needs neither an attach socket nor a writable rootfs (`put_archive` is
refused on this read-only container).

**Unit conversion is a chat capability.** `convert_unit` and `normalize_unit` were
published to MCP clients only. They are offline, read-only and carry no user data, and an
answer about a reading recorded in another unit needs them before comparing or charting,
so they join the chat surface. `resolve_indicator` stays MCP-only.

## Tests

`mirobody/tests/test_chat_auto_citations.py` covers the properties a reader relies on:
the rid is the one the tool minted for that value, the unit stays beside its number,
dates are not mistaken for values, a number no row supports stays uncited and appears in
`auto_uncited`, and an existing citation is not duplicated.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0bb0e4d75521`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.