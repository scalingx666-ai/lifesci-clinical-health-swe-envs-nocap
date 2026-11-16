# Issue

**Title:** feat: add OpenCode one-click install support

## Description

- Add 'opencode' as a supported tool in install.sh
- Handle OpenCode's special path structure:
  - Global: ~/.config/opencode/skills/
  - Project: .opencode/skills/
- Update help text and error messages to include opencode
- Document OpenCode in README.md (badge, table, examples, keywords)
- Add OpenCode paths to technical-guide.md (install paths, lock.json, examples)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1e52e246b1df`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.