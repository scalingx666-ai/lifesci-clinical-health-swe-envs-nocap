# Issue

**Title:** Patient ID partition mode: fix conditional update outside a transaction bundle

## Description

### What was done

Where storage supports an all-partition search, partition selection is deferred to allPartitions and settled once the conditional URL has resolved — a matched update writes to the partition its match already lives in, and doCreateForPostOrPut re-derives and validates the target partition 

Note: Two disabled characterization tests were included to record a separate pre-existing bug: the REST layer's `validateResourceIdAndUrlIdForNonConditionalOperation` discards the user provided body id even for conditional update, making the behaviour violates the [FHIR spec on conditional update](https://www.hl7.org/fhir/http.html#cond-update).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c1ec1d88e920`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.