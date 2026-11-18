# Issue

**Title:** Transfer Options - improve web service and UI

## Description

### Summary

- Include transfer syntax UID in transfer options response
   - `uid` field is added for each transfer syntax in each SOP class, so that it can be presented in the UI
- Tweak transfer option update endpoint to also accept HTTP methods PUT (as well as POST)
- [webapp] Improve Transfer Options submenu
   - show Transfer Syntax UID in each option
   - simplify and restyle form, reduce text
   - have two "Select all" buttons instead of one
      - One of them changes TSes for the selected SOP class, the other one changes all transfer syntaxes. ()

![Screenshot 2023-06-07 164939](https://github.com/bioinformatics-ua/dicoogle/assets/4738426/b25d3469-400f-48cb-bcae-eb1680267cee)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f18b919f81ac`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.