# Issue

**Title:** feat: warn about enabled providers without OAuth credentials

## Description

## What does this change?

Providers now report whether their OAuth client ID and secret are set (`credentials_configured` in `GET /api/v1/oauth/providers`). Settings → Providers shows a warning on enabled providers missing them, and startup logs the same.

## Why?

Every provider is enabled by default, so on most instances some of them show up on the pairing page without credentials and connecting fails. Nothing in the developer portal pointed at the cause.

This only warns. Blocking enabling without credentials and changing the defaults is #1945, and what disabling should actually do is #1944.



## How did you test this?

Local instance with credentials set for some providers only.

`GET /api/v1/oauth/providers`:

```
provider        has_cloud_api  credentials_configured
apple           false          true
garmin          true           true
google_health   true           false
oura            true           false
fitbit          true           false
sensorbio       true           false
withings        true           false
(other providers: true)
```

Startup (`init_provider_settings.py`):

```
⚠ google_health: enabled but OAuth client ID or secret is not set
⚠ oura: enabled but OAuth client ID or secret is not set
⚠ fitbit: enabled but OAuth client ID or secret is not set
⚠ sensorbio: enabled but OAuth client ID or secret is not set
⚠ withings: enabled but OAuth client ID or secret is not set
```

Settings → Providers:

<img width="2880" height="3250" alt="provider-credentials-warning" src="https://github.com/user-attachments/assets/5c722ab9-0ef0-4dbb-b518-1205c399c276" />

Only the client ID and secret are checked. Provider-specific extras like the Suunto subscription key or Google project ID are not.

## AI usage

Claude Code (Claude Opus) for the implementation and the description.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Provider settings now show whether required OAuth credentials are configured, based on the client ID and secret. Providers that do not use OAuth are shown as configured.
  * Enabling a provider with missing credentials displays a warning with steps to resolve the issue or disable the provider.
  * Setup checks now warn when an enabled provider is missing OAuth credentials.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8e2915961b79`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.