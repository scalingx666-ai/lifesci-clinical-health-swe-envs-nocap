# Issue

**Title:** Offer custom welcome messages at the login page

## Description

This provides a nice-to-have: updated, customizable messages for when a user is about to log in to a Dicoogle instance.

<img width="963" height="472" alt="Screenshot_2025-10-11_16-30-17" src="https://github.com/user-attachments/assets/6113f39a-0263-4bdf-b42b-81908ae2a4a2" />

Welcome messages can be described as simple HTML text, each message separated by two consecutive newlines (`\n\n`). If a custom welcome file is not provided, Dicoogle will use an embedded listing which you should take a look in the new file `welcome.html`. Feedback on other messages to provide are welcome.

### Summary

- [server] add `/welcome` servlet
   - returns one of the listed messages at random, content type `text/plain`
   - loads messages from resource file `welcome.html` or from a custom file (`-Ddicoogle.welcomeFile`)
- [webapp] add `domify` dependency to introduce an HTML sanitization step
- [webapp] update login view to show a welcome message from the ones listed

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `83f3b8fd03bc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.