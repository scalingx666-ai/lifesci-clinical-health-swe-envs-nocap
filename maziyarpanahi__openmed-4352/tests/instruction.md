# Issue

**Title:** Refresh verified wheel-size baseline

## Description

Current master fails the wheel-size gate: 7,848,985 bytes exceeds the old 7,739,665-byte maximum. Archived builds and a wheel-member comparison explain 812,926 bytes of accepted library growth since the prior baseline, including 142 added members. All packaged source/resource payloads match the frozen Git revision; model weights and build caches are absent.

Refresh the baseline to the measured master ac3b2df82fa547a395d6b24722e556d32b2b6c2e and the maximum to 8,633,884 bytes. Retain 10% headroom, independent frozen-base CI measurement, package contents, compression and import limits. Document the measurements and growth sources.

Validation on 8c3967c79ae9dd151efedcb9501f13c9c8c52ad2:
- Existing release-budget checks: 29 passed, 16 subtests passed.
- Full suite: 23,009 passed, 151 skipped, 11,220 subtests passed.
- `make format`, `make lint`, `make format-check` passed.
- Strict docs and all three staged-artifact/homepage-beacon/clinical-exclusion browser guards passed.
- Final wheel is byte-for-byte identical to frozen master. Existing core/Chinese/Indic footprint checks and the unchanged clean-wheel import budget passed.
- Independent Ubuntu build passed on the exact SHA: frozen base reproduced at 7,848,985 bytes with SHA-256 c6aac5686e941ebcd5ea6c563c807e9f9bcc27473dfe8e1d8e87efa61c38b166. Hosted footprint/import checks and all 25 applicable checks passed; 46 label-event checks skipped.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ac3b2df82fa5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.