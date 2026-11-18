# Issue

**Title:** Remove five unreferenced frontend modules

## Description

### Description of Change

**Link to GitHub issue or Jira ticket:** none - noticed while reading the frontend code.

**Description:**

Two modules under `src/js` that nothing imports:

- `consts/imagesUrls.js` - autosave feature-bar image path
- `consts/dataFormat/numberData.jsx` - hardcoded dashboard sample data

Nothing references either one - checked `src/js` and `grails-app`
(including `.gsp` templates), the dynamic imports in `Router.jsx`, the
tests, and the webpack, jest and styleguide configs. The `numberData`
prop in `Dashboard.jsx` comes from the redux `indicators` state, not from
the deleted file.

This PR originally proposed five files. Following @alannadolny's review,
`consts/autosaveStatuses.jsx`, `consts/transactionType.js` and
`utils/FormatDate.jsx` are kept, and the comment edit in
`consts/dateFormat.js` is reverted since it referred to `<FormatDate>`,
which stays.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `85a3864b3041`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.