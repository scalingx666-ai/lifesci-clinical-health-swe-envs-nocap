# Issue

**Title:** chore(ci): use foomedical's own Google client ID and reCAPTCHA key for foomedical.com

## Description

#11271 pointed the foomedical.com deploy at `secrets.STAGING_GOOGLE_CLIENT_ID` and `secrets.STAGING_RECAPTCHA_SITE_KEY`. This switches it back to foomedical's own Google client and reCAPTCHA key, now read from the `FOOMEDICAL_GOOGLE_CLIENT_ID` and `FOOMEDICAL_RECAPTCHA_SITE_KEY` repository variables. They hold the values that were hardcoded before #11271.

Foomedical PR previews in `build.yml` keep the staging secrets, since they're served from preview.medplum.dev.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `436d8614211a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.