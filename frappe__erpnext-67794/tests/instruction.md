# Issue

**Title:** fix: keep custom primary buttons readable on hover

## Description

Depends on frappe/frappe#47604.
Related to issue :  frappe/frappe#46765

### Problem

https://github.com/user-attachments/assets/958a5b68-855c-4c16-a265-e86f9dde81e4

Custom buttons with `.addClass("btn-primary")` fade on hover. The text stays white on a light background. 


### Solution
https://github.com/user-attachments/assets/bf51e5d9-1b09-41f4-b32e-c97156e72a25

This PR passes `"primary"` as the new `type` argument of `add_custom_button` instead, so the buttons render as solid and stay readable in light and dark mode. 15 call sites in 12 files.
Please review with **Hide whitespace**, because Prettier re-wraps the calls.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `676813027fee`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.