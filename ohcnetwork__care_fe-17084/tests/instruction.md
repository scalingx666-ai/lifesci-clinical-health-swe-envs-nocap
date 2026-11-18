# Issue

**Title:** Drop unused env options and sync env schema, types and examples

## Description

## Proposed Changes

3.1 removed the UI that used some configuration options, but the options were still defined, typed, validated and documented. This removes them, and fixes the places where `care.config.ts`, `src/vite-env.d.ts`, `scripts/validate-env.ts` and `.example.env` had drifted apart.

### Removed (no consumers left)

| Option | Why |
|---|---|
| `REACT_GITHUB_URL` → `careConfig.urls.github` | Only `AuthHero` used it. 3.1 replaced `AuthHero` with `AuthLayout`, which has no GitHub link. |
| `careConfig.customDescription` | Never read. `REACT_CUSTOM_DESCRIPTION` itself **is kept**: `vite.config.mts` renders it to sanitized HTML as `__CUSTOM_DESCRIPTION_HTML__`, which the `AuthLayout` footer shows. |
| `REACT_APP_COVER_IMAGE_ALT` | Unused since the Vite migration (`index.html` only uses `REACT_APP_COVER_IMAGE`), yet validation required it. |
| `CARE_CDN_URL`, `ESLINT_NO_DEV_ERRORS` (`.env`) | Nothing reads them. The CSP uses `REACT_CDN_URLS`, and there is no ESLint Vite plugin. |

Plugins only get `careConfig` through `window.__CORE_ENV__`, and none of the plugin repos I checked read the removed keys. They only use `apiUrl`.

### Synced
- **`REACT_DEFAULT_PAYMENT_TERMS`** is now read through `careConfig.defaultPaymentTerms`, not `import.meta.env` directly in `CreateInvoice`.
- **New validation:**
  - `REACT_DEFAULT_PAYMENT_METHOD`: must be a `PaymentReconciliationPaymentMethod`.
  - `REACT_TOAST_POSITION`: must be a valid position.
  - `REACT_MEDICATION_VALUE_SET_SELECT_DEFAULT_TAB`: `product` or `valueset`.
  - `REACT_APP_RESEND_OTP_TIMEOUT`: positive number.
  - `REACT_APPOINTMENTS_USE_AVAILABILITY_STATS_API`: boolean.
  - `REACT_MFE_REGISTERED_COMPONENTS`, `REACT_INJECTED_HEAD`, `REACT_INJECTED_HTML`: strings.
- **Types:** every env var read by `care.config.ts` is now declared in `vite-env.d.ts`. Typing `REACT_PATIENT_REGISTRATION_DEFAULT_GEO_ORG` as `string | undefined` exposed an unchecked `setValue` in `PatientRegistration`, now guarded. The picker reads `_selected_levels[0] ?? null`, so behaviour is unchanged.
- **`.example.env`:**
  - Added `REACT_SBOM_BASE_URL`, `REACT_CDN_URLS`, `REACT_MFE_REGISTERED_COMPONENTS`, `REACT_INJECTED_HEAD/HTML`, `REACT_DEFAULT_COUNTRY_NAME`, `REACT_OBSERVATION_PLOTS_CONFIG_URL`, `REACT_APPOINTMENTS_USE_AVAILABILITY_STATS_API` and `REACT_ENABLE_TOKEN_GENERATION_IN_PATIENT_HOME`.
  - Corrected the docs for `REACT_DEFAULT_ENCOUNTER_TYPE`, which has no `hh` default.
  - Corrected the docs for `REACT_INVENTORY_EXPIRY_MONTH_OFFSET`. It must be a positive integer or unset; the example previously set `0`, which fails validation.
- **Sentry:** removed the hardcoded `Sentry.init` in `index.tsx`. In production it ran alongside `Integrations.Sentry`, and until the app mounted it sent errors to the OHC DSN even when a deployment had set its own `REACT_SENTRY_DSN`. Sentry is now configured only from `REACT_SENTRY_DSN`/`REACT_SENTRY_ENVIRONMENT`, which default to the same DSN.
- **`.github/copilot-instructions.md`:** removed the reference to `REACT_ENABLE_HCX`, which no longer exists, and fixed the `.env` description (it is committed) and the local test API URL.

### Things deployers should know
- Deployments that still set a removed variable keep building, because `z.object` ignores keys it doesn't know.
- An invalid `REACT_DEFAULT_PAYMENT_METHOD`, `REACT_TOAST_POSITION`, `REACT_MEDICATION_VALUE_SET_SELECT_DEFAULT_TAB`, `REACT_APP_RESEND_OTP_TIMEOUT` or `REACT_APPOINTMENTS_USE_AVAILABILITY_STATS_API` now **fails the build**. Before, it fell back with a console warning or was used unchecked.
- Errors thrown before `<App />` mounts are no longer sent to Sentry.

### Verification
- `npx tsc --noEmit` and `npm run build` pass.
- ESLint on the changed files: no errors (warnings only, all pre-existing).
- Ran `validateEnv` against the committed `.env` plus overrides. Valid values for every new rule pass; invalid values fail with the expected message (payment method, toast position, medication tab, OTP timeout `0`, stats flag `yes`, expiry offset `0`).
- The production bundle now contains the Sentry DSN only once, as the `careConfig.sentry` default.

### Not in this PR
`.example.env` as a whole still fails validation if copied verbatim, because empty `KEY=` lines are checked as `""` (e.g. `z.url()` rejects `""`). Fixing that means deciding how empty values are treated in both `validate-env.ts` and `care.config.ts`. For example, an empty `REACT_ALLOWED_ENCOUNTER_CLASSES` currently becomes `[""]`.

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a37f4330571b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.