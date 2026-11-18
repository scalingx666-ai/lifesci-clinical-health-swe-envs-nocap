# Issue

**Title:** Update react-bootstrap-table to v3

## Description

This PR updates the dependency `react-bootstrap-table` to the latest v3: 3.5.1.

This update is relevant because it reduces the total JavaScript bundle size from 1.5MB to 1.14MB, as a consequence of now being able to minify the dist code of this dependency properly. The production bundle constructed via  Webpack no longer contains calls to `eval`.

- update dependency + css file
- instruct webpack to resolve `global` to `window`
- replace deprecated use of `ReactBootstrapTable.Input`
- update `SearchResult` prop types
- remove statement of deprecation of `SearchResultView` (since it's not true)

- in progress: let the user go forward in the result steps if a previous selection at the same level had been made

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cdd0e79bee00`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.