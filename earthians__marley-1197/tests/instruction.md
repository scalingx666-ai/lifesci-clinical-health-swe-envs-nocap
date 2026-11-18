# Issue

**Title:** fix: scope Patient Progress layout CSS to its own page

## Description

## Problem

Same class of bug as #1194, in the sibling page. `patient_progress.css` overrides the core desk classes `.layout-side-section` and `.layout-main-section-wrapper` without any page scope:

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

So a single visit to Patient Progress leaves every subsequent desk page — workspace, list view, form view — capped at `max-width: 80%` with a force-shown sidebar, until a full browser reload.

Both blocks were added to the two pages together in #882; #1194 fixed only the Patient History copy.

### Steps to reproduce

1. Open any workspace / list / form — renders at full width
2. Navigate to `/app/patient-progress`
3. Navigate back to the workspace
4. Content is now squeezed into 80% of the viewport with a blank strip on the right
5. Only `Ctrl+Shift+R` restores it

## Fix

Scope both rules to the page container (`#page-patient_progress`, set by `frappe/public/js/frappe/views/container.js:30-32`), identical to the fix merged in #1194.

Behaviour on the Patient Progress page itself is unchanged — the added ID raises specificity, so the rules still win where they are meant to.

**2 lines changed, 1 file.** No build step required: desk page CSS is read from disk per request, not bundled.

## Testing

1. `bench --site <site> clear-cache`, then hard-reload the browser
2. Desk workspace renders full width
3. Visit Patient Progress — sidebar and 80/20 split render correctly
4. Back to workspace / list / form — still full width

## Notes

Out of scope for this minimal fix, but still present in this file: several generic selectors are declared globally and leak the same way — `text.title`, `.date-field .clearfix`, `.date-field .help-box`, `.date-field .form-group`, `.chart-filter-search`, `.chart-control`, and `.layout-side-section .frappe-control[data-fieldname="patient"]`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ee8772a562fc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.