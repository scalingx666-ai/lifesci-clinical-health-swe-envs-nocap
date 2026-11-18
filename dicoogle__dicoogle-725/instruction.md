# Issue

**Title:** Fix logout and root page loading dynamics

## Description

### Summary

- [webapp] Fix runtime error when trying to log out
   - It was a mistake in the retrieval of the router history object
- [webapp] Fix nuances of loading of root page when the user navigates to `/#/` directly
   - Remove the loading page as an index route
   - Route to login page only after fetching from user store (even when there is no user session on local record)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d3a98a770722`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.