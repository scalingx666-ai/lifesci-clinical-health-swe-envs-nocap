# Issue

**Title:** fix: scope Patient History layout CSS to its own page

## Description

## Problem

`patient_history.css` overrides the core desk classes `.layout-side-section` and `.layout-main-section-wrapper` without any page scope:

```css
.layout-side-section {
	display: block !important;
	padding: 10px;
	width: 20%;
	flex: 0 0 20%;
}

.layout-main-section-wrapper {
	flex: 1;
	width: 80%;
	max-width: 80%;
}
```

Both classes are emitted for **every** desk page by `frappe/public/js/frappe/ui/page.js:102-114`.

The override leaks globally and persists, because:

1. `Page.load_assets()` reads the page's `.css` into `Page.style` — `frappe/core/doctype/page/page.py:161-165`
2. `pageview.js:91` injects it via `frappe.dom.set_style(this.pagedoc.style || "")`
3. `frappe.dom.set_style()` is called **without an `id`**, so it appends a fresh `<style>` to `<head>` with no teardown on route change — `frappe/public/js/frappe/dom.js:95-115`

So a single visit to Patient History leaves every subsequent desk page — workspace, list view, form view — capped at `max-width: 80%` with a force-shown sidebar, until a full browser reload.

### Steps to reproduce

1. Open any workspace / list / form — renders at full width
2. Navigate to `/app/patient_history`
3. Navigate back to the workspace
4. Content is now squeezed into 80% of the viewport with a blank strip on the right
5. Only `Ctrl+Shift+R` restores it

## Fix

Scope both rules to the page container (`#page-patient_history`, set by `frappe/public/js/frappe/views/container.js:30-32`).

Behaviour on the Patient History page itself is unchanged — the added ID raises specificity, so the rules still win where they are meant to.

**2 lines changed, 1 file.** No build step required: desk page CSS is read from disk per request, not bundled.

## Testing

1. `bench --site <site> clear-cache`, then hard-reload the browser
2. Desk workspace renders full width
3. Visit Patient History — sidebar and 80/20 split render correctly
4. Back to workspace / list / form — still full width

## Notes

Out of scope for this minimal fix, but worth a follow-up in the same file:

- Generic utility classes are also declared globally: `.d-flex`, `.p-3`, `.mt-2`, `.mr-3`, `.py-3`, `.width-full`, `.avatar`, `.Box`, `.border-bottom`, `.flex-column`
- The `#page-medical_record` rules are dead — that page ID no longer exists

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ac8a3006ca37`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.