# Issue

**Title:** Fix requesting for web UI plugins by slot

## Description

In a permissive setting, webcore would fetch all plugins regardless of type, causing instability in the process.

For testing, consider enabling the `webui.permissive` JVM variable (`-Dwebui.permissive=1`), so that all web UI plugins appear regardless of RBAC policies.

- remove service_get, replace all uses
   - fetchPlugins can use getWebUIPlugins instead
   - use Dicoogle.request directly on issueSearch

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0fe549ece131`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.