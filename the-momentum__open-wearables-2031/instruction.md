# Issue

**Title:** fix(backend): keep credentials out of Sentry events

## Description

Plug several paths through which credentials reached Sentry in plain text: the developer API key header, an Oura access token in error messages, provider secrets in outgoing request breadcrumbs, and OAuth tokens in event data. Credentials are now masked both in the default mode and with sensitive data sending enabled.

## Changes

- Mask the custom developer API key request header in Sentry events; the SDK only strips standard auth headers and matches header names exactly.
- Treat client secrets, PKCE code verifiers, ID tokens, access tokens and refresh tokens as credentials, so they stay masked also when sensitive data sending is enabled (previously some were masked only as PII, and access/refresh tokens not at all).
- Stop the Oura token revoke failure from carrying the access token: the provider takes the token as a query parameter, which the HTTP client renders into the error message and its exception chain.
  _(Changed during review by Sebastian Kalisz:)_ The failure is raised as a `ProviderError` ("Oura API error (status N)", or "Oura API request failed" without a response) with the provider's status, like other provider calls, instead of a bare `RuntimeError`.
- Mask query strings of outgoing HTTP requests in breadcrumbs and performance spans, which carried the Oura token and Strava client credentials; the request path stays visible.
- _(Added during review by Sebastian Kalisz:)_ With sensitive data sending enabled, the query string of incoming requests had no masking at all. Its credential parameters (the OAuth callback `code`, webhook verification tokens) are now masked in error events and sampled transactions, other values stay visible; raw ASGI scopes in frame locals no longer carry the query string.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Sensitive credentials—including API keys, access and refresh tokens, OAuth credentials, and tokens in recognized query parameters—are now masked in error reports and transactions. Request headers and raw request data are also scrubbed in sensitive-data reporting mode; unrelated query values remain visible where supported.
  * Oura token revocation failures now return sanitized errors: HTTP failures include the status code, while other request failures use a generic message. Original exception details are not chained, and successful revocations continue to work.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `74a817da085f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.