# Issue

**Title:** Update CI workflows

## Description

### Summary

- update actions to latest versions
   - removes use of Node.js 12 in workflows, which is deprecated and will stop working soon
- fix step descriptions
- change trigger conditions based on paths of files changed
- [maven.yml] configure maven caching via setup-java, thus simplifying workflow specification
- [node.js] update node-versions to stay up to date over time
- [node.js] bump minimum node version to 16
- [node.js] add npm caching
- Add npm check script
- [CI] Run check script in node workflow

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `90fea3507765`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.