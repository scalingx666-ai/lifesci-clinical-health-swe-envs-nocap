# Issue

**Title:** Contain native media decoder probes and resource failures

## Description

## Description

.

Contain malformed or resource-exhausting media probes in disposable workers so native decoder crashes cannot take down the calling process or leave raw media output. Inputs are bounded bytes, and results contain fixed categories, hashes and counts only.

## Changes

- Add closed PDF, TIFF, native DICOM, WSI TIFF, PCM WAV and video probes using installed optional decoders. No filename, URL, arbitrary executable or provider callback is accepted.
- Require Linux resource limits and a native-ABI syscall filter before decoding. Bound address space, CPU, wall time, geometry and decoded work; deny writable opens, file mutations, sockets, process creation, execution and resource-limit changes. Disable dumpability as well as core-file output.
- Feed input through a bounded pipe, retry transient backpressure, suppress native stdout/stderr, terminate the owned process group on cancellation/timeout and reap the worker. Unsupported isolation and missing backends fail closed.
- Reject cyclic or out-of-bounds classic/BigTIFF directory graphs before native decoding. Keep parser errors, resource failures and unmeasured capability explicit.
- Add a minimal synthetic fixture generator and real crash, memory/CPU exhaustion, timeout, denied I/O and parent-recovery controls, plus a guide, changelog and reviewed operational/network inventories.

This is crash/resource containment, not a complete OS sandbox or malware scanner. The installed interpreter/libraries are trusted and readable host files still require deployment-level isolation. A completed probe is not sanitization, clinical approval or a destruction receipt. Existing ingestion providers are not automatically rerouted. macOS/Windows refuse worker execution; native Linux x86-64/AArch64 are eligible only when every control installs successfully.

## Dependencies

Built from current `master` (`29ffa7005`) with existing #4414 and #4390 prerequisite histories preserved. Original PR branches are unchanged. No dependency or lockfile change is introduced; optional pikepdf, Pillow, pydicom/NumPy and PyAV are supplied by the caller in the local worker environment. No codec wheels, model weights or clinical media are bundled.

## Validation

- 35 actual Linux ARM64 integration controls passed with **all optional backends required**, in a disposable container with no network, read-only mounts, a bounded RAM-only pytest temp directory, no added capabilities and a 1 GiB container ceiling. Includes actual native decoding, crashes, CPU/memory exhaustion, cyclic containers, compressed expansion and pipe backpressure.
- Full Python suite: 25,656 passed, 186 skipped and 11,361 subtests passed. Its only failure was the new guard's private socket-denial control missing from the reviewed network inventory. Added the documented entry, then reran the complete affected telemetry file and guard suite: 13 passed, 32 Linux-only cases skipped on macOS.
- Frozen Python 3.11 validates the unsupported-host refusal path. Linux skips are reported explicitly and are not counted as native containment evidence.
- Canonical format/lint/format-check/type checks, explicit module mypy, public API compatibility and scoped pre-commit hooks passed.
- Strict documentation build and final Pages route, asset, metadata and feed gates passed. The exact guide example executed successfully under Linux containment.
- Final wheel/sdist build and Twine checks passed; both contain byte-exact corrected decoder source. Complete incoming attribution is checked before push; hosted checks will run on the exact PR head.

Type: feature, integration regression controls and documentation. The Python process-isolation boundary is explicitly scoped; existing Swift and backend contracts remain unchanged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5f3a3c864e26`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.