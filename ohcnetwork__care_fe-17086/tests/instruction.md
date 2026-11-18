# Issue

**Title:** Use feature detection instead of UA sniffing for unsupported browser warning

## Description

Supersedes #17085.

## Problem

Chrome 156 on iOS shows the **"Unsupported Browser"** banner: _"Your browser (Chrome version 156) is not supported…"_, even though it's the latest version.

## Why this happens

`BrowserWarning` used two different libraries for two different jobs:

1. **The check** used `src/supportedBrowsers.ts`, a regex that `browserslist-useragent-regexp` generated at build time from our `browserslist` query.
2. **The message** used `bowser` to name the browser and its version.

Browsers on iOS identify themselves with their own user-agent tokens: `CriOS/` (Chrome), `FxiOS/` (Firefox), `EdgiOS/` (Edge). They don't send `Chrome/`, `Firefox/` or `Edg/`. The regex library (via `ua-regexes-lite`, unchanged since Dec 2023) has no patterns for these tokens. It recognises iOS browsers only through the iOS version in the user agent (`iPhone OS 18_6`).

In **desktop mode** (the default on iPad, and "Request Desktop Site" on iPhone), the browser sends a Mac user agent with no iOS version:

```
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) CriOS/156.0.7000.0 Safari/604.1
```

Nothing in that string matches the regex. Bowser does understand `CriOS` and correctly reports "Chrome 156", so the warning ends up naming a current browser.

The deeper problem is that a user agent is a poor stand-in for what a browser can do. iOS-specific tokens, desktop mode, in-app webviews and the user-agent string reduction in Chrome and Safari all break this kind of check. MDN advises using feature detection instead.

## Fix

`BrowserWarning` no longer reads the user agent. It checks for the platform features our styles depend on. Tailwind CSS v4's output uses all four of these (checked in `node_modules/tailwindcss`):

| Feature | Check |
| --- | --- |
| Cascade layers (`@layer theme, base, components, utilities`) | `"CSSLayerBlockRule" in window` |
| `@property` (registered `--tw-*` properties) | `"CSSPropertyRule" in window` |
| `oklch()` colors (default palette) | `CSS.supports("color", "oklch(0% 0 0)")` |
| `color-mix(in oklab, …)` (opacity modifiers) | `CSS.supports("color", "color-mix(in oklab, red, blue)")` |

Together these match [Tailwind v4's documented minimums](https://tailwindcss.com/docs/compatibility): Chrome 111, Safari 16.4 and Firefox 128. Those are also stricter than the JavaScript build target (`es2022`). Browsers that pass the checks are the ones our styles render correctly in, whatever user agent they send.

The message no longer names a browser or version, since there's no user agent to parse. It now says the browser is missing features the app needs. It uses a new i18n key (`unsupported_browser_features_description`) so existing translations, which interpolate `{{name}}`/`{{version}}`, aren't shown with the wrong meaning.

### Removed

- `scripts/generate-supported-browsers.mjs`, the `supported-browsers` npm script and its calls in `dev`, `local` and `build`
- The "Generate supported browsers" CI step, plus the `.gitignore` and `knip.json` entries for `src/supportedBrowsers.ts`
- Dependencies: `bowser`, `browserslist-useragent-regexp` and the direct `browserslist` dependency, which only existed for the generator. Six more packages drop out of the lockfile with them.

The `browserslist` **config field** in `package.json` stays, because workbox's Babel step (`@babel/preset-env`) reads it when building the service worker.

### Note on `en.json`

The pre-commit `sort-locales` hook re-sorted several keys recently merged out of order into `3.1/base`. The only real change in that file is replacing `unsupported_browser_description` with `unsupported_browser_features_description`.

## Testing

- `npm run typecheck`, ESLint and Prettier pass.
- knip shows no new issues. It only lists two untracked local `floorplan/` files that aren't part of this branch.
- I ran the detection expression in real engines through Playwright:
  - Chromium 149: `true`
  - WebKit 26.5: `true`
  - Firefox: couldn't launch locally (timed out), not verified
  - As a sanity check, `CSS.supports` returns `false` for a made-up color function in both Chromium and WebKit.
- I haven't checked the banner on a real iOS device or an old browser.

## Out of scope

A browser that can't parse the `es2022` bundle never runs React, so it never reaches this check (the old one had the same gap). Covering that case would need a script that runs before the bundle, in `index.html`. That interacts with the CSP header (currently report-only, `default-src 'self'`), so it's left for a follow-up.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `db0361fd84ae`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.