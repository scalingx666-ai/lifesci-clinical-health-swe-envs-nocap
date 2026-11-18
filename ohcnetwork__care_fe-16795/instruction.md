# Issue

**Title:** Adds support for running vite-server using `portless`

## Description

### Proposed changes

- Adds support for running vite-server using [portless](https://portless.sh/)
- `portless` uses `PORT` env var to set 
- Why/how this helps in development: https://portless.sh/why


<img width="1039" height="1364" alt="image" src="https://github.com/user-attachments/assets/224f8fc3-b4b6-45ef-b867-53984c767426" />

<img width="1068" height="836" alt="image" src="https://github.com/user-attachments/assets/dc3e1f41-97f9-409a-885d-55a299825599" />


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

- **New Features**
  - Local development and preview servers now support a configurable port, defaulting to port 4000 when none is specified.
  - Explicitly configured ports are enforced to ensure the application starts on the requested port.
  - Added streamlined startup support for serving the app through a stable local URL on an available port.

- **Documentation**
  - Updated development documentation with instructions for the preferred startup method and the direct localhost fallback.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b442bfbd5428`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.