# Issue

**Title:** Mute finalized spoken identifiers in retained audio

## Description

Create a separate silent-range copy of one already screened PCM utterance under its original retention deadline. The source is unchanged. Source and derivative are separate expected artifacts with destruction receipts bound to the same inventory.

Bind the capture and final screening digests, check the complete character-to-token coverage, and round padded ranges out through the ASR and original sample rates. Copy only unredacted intervals into a zeroed buffer and verify every channel. If only reliable whole-utterance bounds are available, the caller can explicitly mute the entire utterance. Missing, uncertain or stale evidence refuses the derivative. The report contains only ranges, counts and digests.

. Uses the retention and withholding contracts from #4401. The feature is the five-file change in `0851cd57a`. No new dependencies or bundled recordings.

**Validation:** `pytest tests/unit/multimodal/streaming/privacy/ -q` (98 passed on the final commit), including actual final screening, stereo sample comparisons, refusal and destruction receipts. Full offline Python suite before the final additional timing check: 25,752 passed, 155 skipped. Ran `make format lint format-check type-check docs-build`, targeted mypy, public API compatibility, scoped pre-commit, wheel/sdist build and Twine, committed-history secret scan, and attribution over all ten incoming commits. See the updated audio retention guide for caller responsibilities and the limitations of muting detected identifiers.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `26d6f1a8e852`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.