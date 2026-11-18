# Issue

**Title:** feat: add offline multimodal preflight CLI

## Description

## Description
Add `openmed multimodal preflight` for a local file or an explicitly enabled, bounded directory scan. The installed argparse CLI and optional Typer CLI share deterministic JSON, opaque asset IDs and fixed diagnostics without filenames or source content.

PNG, JPEG, classic TIFF and WAV use existing bounded header readers. PDF geometry and DICOM-prefix evidence remain conservative: missing raster geometry or frame metadata holds admission instead of inventing support. No decoding, inference, downloads or input writes occur.

## Type of Change
- [x] New feature
- [x] Tests and documentation

## Changes Made
- Compose actual manifests, digests, metadata profiles, per-file ceilings and ordered batch preflight reports; preserve filesystem failures without fabricated manifests.
- Bound enumeration, depth, result count, reserved file bytes and actual read work. Continue across individual failures and retain explicit aggregate and duplicate findings.
- Reject symlinks throughout POSIX paths using held directory descriptors. On Windows, reject reparse points and hold ancestor/file handles without write/delete sharing.
- Include the new tests in the existing Windows/macOS portability jobs.
- Add the CLI guide, navigation, publication registration and changelog.

## Dependencies and merge order
This branch preserves Rudy Celekli's original #4173 batch-preflight commit and integrates it with current master. Merge #4173 first, then refresh and revalidate this PR. The original contributor branch is unchanged. A small maintainer follow-up makes batch accumulator types explicit without changing behavior.

The branch also carries the independently validated scanner-install and documentation-search accessibility repairs used by the other v3.3 implementation PRs. No package dependencies or lockfile changes.

## Testing
- [x] Focused CLI and batch tests: **64 passed, 1 Windows-only skip**, on Python 3.12 and the frozen Python 3.11 environment.
- [x] Full suite: **25,628 passed, 156 skipped, 11,361 subtests passed**, 78 warnings, 195.98 seconds.
- [x] `make format lint format-check type-check`; explicit module mypy, including Windows platform types.
- [x] Strict `make docs-build`, publication metadata, routes and feeds.
- [x] Existing documentation controls passed in Chromium, Firefox and WebKit.
- [x] Wheel and sdist built; source bytes verified against this implementation; `twine check` passed.
- [x] API compatibility, dependency-license policy, actionlint, pre-commit security/secret checks and all five incoming commits' attribution policy passed.

Negative controls cover malformed headers, missing metadata, private error strings, empty/over-limit directories, byte limits before reads, growing/changed files, duplicate content, symlink and ancestor replacement races, FIFO refusal, and fresh-process execution without decoder imports or network calls. Hosted Windows execution is still required; the local Windows-specific handle test was skipped on macOS.

## Documentation
- [x] Public docstrings, guide and changelog updated.
- [x] Limits and conservative PDF/DICOM outcomes documented.

## Related Issues

Related to #3009, #4173

## Example
```bash
openmed multimodal preflight ./synthetic-input.png
openmed multimodal preflight ./synthetic-packet --directory --profile mobile
```

Exit 0 means admission, 1 means hold and 2 means invalid invocation. Admission is a bounded metadata/resource check, not clinical validity, complete encoding validation, malware scanning or proof that redaction succeeds.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6ddddbf27883`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.