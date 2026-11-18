# Issue

**Title:** fix(patient-portal): give the patient portal RTL text direction and logical spacing

## Description

## Problem

`healthcare/www/patient_portal.html` is a standalone HTML document — unlike most Frappe web pages it does not `{% extends "templates/web.html" %}`, so it inherits none of `base.html`'s `dir`/`lang` handling. It renders a hardcoded `<html lang="en">` for every user, so Arabic (and other RTL-locale) patients get left-to-right layout with no way for a site admin to fix it.

## Fix

Supply the same two boot keys, from the same sources, as `crm/www/crm.py`:

```python
"lang": get_user_lang(),
"text_direction": "rtl" if is_rtl() else "ltr",
```

and bind them in the template:

```html
<html lang="{{ boot.lang }}" dir="{{ boot.text_direction }}">
```

`is_rtl()` is Frappe's own Jinja global (ar/he/fa/ps) — this follows the same convention already used by builder, crm, drive, gameplan, insights and wiki, rather than inventing a new one.

`patient_portal/public/index.html` is deliberately **not** touched — it's the Vite dev-server entry (the build's `outDir` is the assets dir, not this file), so it's never Jinja-processed and `{{ boot.lang }}` would render as a literal, unresolved brace in dev.

## Second commit — logical spacing

Setting `dir="rtl"` mirrors text but a few hardcoded physical-spacing classes (`mr-`, `pr-`) in `AppointmentModel.vue` / `DiagnosticModel.vue` don't follow, leaving icon/content spacing running left-to-right inside an otherwise-mirrored layout. Swapped to the logical equivalents (`me-`, `pe-`) — behavior-preserving for LTR (they resolve to the same physical side), and correct for RTL. `patient_portal` is on Tailwind 3.4.15, well past the 3.3 release that introduced logical-property utilities.

## Testing

Verified on Frappe 16.26.3: both imports resolve, `is_rtl()` returns True/False as expected for RTL/LTR locales, and zero physical spacing classes remain in `patient_portal/`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `43216a673488`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.