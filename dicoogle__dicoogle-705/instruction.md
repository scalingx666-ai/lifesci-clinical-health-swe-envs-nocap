# Issue

**Title:** Make ControlServices comply with autostart server settings

## Description

- do not start the service(s) if their respective autostart setting is set to false, a regression probably existing since Dicoogle 3.0.0
- remove unused variable `webServicesRunning` in `ControlServices`
- remove use of raw types in `startStorage()`
- remove outdated TODO note
- refactor `ControlServices#startStorage()` to return whether the service started (`true`) or was already running (`false`) and raise an exception on error
- adjust `ServicesServlet` according to changes to `ControlServices`, and for the output to be more precise and informative

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `15c65f503932`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.