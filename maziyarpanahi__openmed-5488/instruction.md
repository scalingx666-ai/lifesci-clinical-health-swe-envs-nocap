# Issue

**Title:** Fix Nix CLI tests and pinned image signer downloads

## Description

## Description

Keep the offline multimodal CLI tests working in the Nix dev shell and restore the published image-signing job after the upstream download endpoint returned HTTP 504.

## Type of Change

- [x] Bug fix
- [x] Test improvement

## Changes Made

- Preserve the parent Python dependency search path in both CLI subprocess tests.
- Fetch the same Cosign v3.0.6 Linux binary and its release signature bundle through the official GitHub asset API. Check the pinned digests before execution and verify the original Sigstore publisher identity and issuer.
- Seed the existing pinned Syft action with the checksum-verified v1.42.3 archive. The image digest lookup, signing, attestation, and verification steps are identical.

## Testing

- Reproduced all five CLI failures with a bare interpreter supplied dependencies via PYTHONPATH. All five passed after the fix.
- Ran the signing workflow tests, actionlint, make format, make lint, make format-check, and the full local Python suite.
- Verified the exact Linux signer and signed bundle with Cosign v3.0.6. The signature check rejected a different payload.
- Started the existing hosted Nix workflow on this branch.

## Dependencies

Uses the same signer and SBOM tool versions as the last successful signing job.

## Related Issues

, and #5476.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c45930a85825`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.