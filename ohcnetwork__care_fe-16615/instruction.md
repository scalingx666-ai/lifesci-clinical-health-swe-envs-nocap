# Issue

**Title:** [ENG-874] Allow empty REACT_CARE_API_URL for relative same-origin API requests

## Description

ENG-874

## Change

Permit an empty `REACT_CARE_API_URL` value. An empty value makes the frontend send relative, same-origin API requests.

## Why this works

The frontend already supports this. `care.config.ts` sets `apiUrl` to `env.REACT_CARE_API_URL ?? ""`. The client makes each request as `` `${apiUrl}${path}` ``. The `path` starts with `/api/v1/...`. So an empty `apiUrl` gives a relative request. The request goes to the origin that served the page. Only the build-time check stopped this value.

## What this PR changes

`scripts/validate-env.ts`:
- `REACT_CARE_API_URL` accepts an empty string or a URL.
- The check fails only when the value is not set and `REACT_CARE_URL_MAP` is also not set.
- An empty value is a permitted choice.

`.example.env`:
- Shows that an empty value selects relative, same-origin requests.

The client code does not change.

## When to use this

Use an empty value when one reverse proxy serves the frontend and the API on the same origin. The proxy sends `/api` to the backend. Relative requests are correct in this setup. They also work when you open the box from more than one origin (a LAN name, a LAN IP, or a VPN name). You do not have to list each origin in `REACT_CARE_URL_MAP`.

## Behavior

| `REACT_CARE_API_URL` | `REACT_CARE_URL_MAP` | Result |
| --- | --- | --- |
| not set | not set | Error (no change) |
| not set | set | Use the map (no change) |
| a URL | any | Use the URL or the map (no change) |
| empty | not set | Relative same-origin (new) |
| empty | set | Use the map; empty is the fallback (new) |



<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added support for using relative same-origin `/api` requests when no API URL is configured.

* **Documentation**
  * Documented how to leave `REACT_CARE_API_URL` empty when a reverse proxy serves both the frontend and API.

* **Bug Fixes**
  * Updated environment validation to allow an intentionally empty API URL while still reporting missing configuration when required.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `47abd7fa045b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.