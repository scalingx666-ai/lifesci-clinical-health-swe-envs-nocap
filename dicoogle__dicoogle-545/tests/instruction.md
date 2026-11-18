# Issue

**Title:** Updated restlet url to https://maven.restlet.talend.com

## Description

The Maven Restlet dependency URLs have become deprecated, and the associated certificates have become invalid since December 11th, making it an insecure connection which fails Maven installations.

This PR replaces the Dicoogle and Dicoogle SDK Restlet dependency URLs to the current URL: `https://maven.restlet.talend.com`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `35401d82f6b8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.