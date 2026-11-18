# Issue

**Title:** Fix ExportCSVToFILEServlet query expansion handling

## Description

Continued from #549. We can instead fix the export servlet to behave exactly like the search servlet here.

- ignore "keyword" parameter, add opt-in "expand" parameter instead

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e1fe1a299be8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.