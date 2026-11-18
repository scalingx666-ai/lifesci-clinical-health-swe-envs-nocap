# Issue

**Title:** fix: limit keyboard shortcuts to the topmost overlay

## Description

## Proposed Changes

. All of these reproduce on `3.1/base` today.

**Shortcuts could click through a modal**

- `resolveBestHost` accepted a host in any open overlay. #17016 added `[data-open]` to the overlay selector, which brought shortcuts back inside Base UI overlays and exposed this.
- With the dispense "Change Location?" warning open, `Shift+Enter` clicks **Confirm Dispense** behind it and sends the dispense request.
- Shortcuts now reach only the topmost open overlay. If that overlay has no matching host, nothing happens.

**Shortcuts fired behind open dropdowns and menus**

- Base UI select and menu popups weren't in the overlay selector, so they never blocked anything. They count as overlays now.
- An empty dropdown and a menu opened with the mouse keep focus on the popup, so the key reaches the page. `Shift+Enter` with **Blood Group** open clicks **Register Patient**, and `Enter` with the menu beside **Collect Payment** open opens Collect Payment behind it.
- `Shift+ArrowLeft` got through even with an option focused, which left the form with a dropdown still open.

**Page shortcuts fired behind the page actions palette**

- The palette's exemption from the overlay guard applied to every shortcut, not just to actions chosen from it. With focus off the search box, pressing `E` on an account opened Edit Account behind the palette.
- Now only actions chosen from the palette skip it (`fromCommandDialog`). Keyboard shortcuts stay blocked.

**The palette listed actions that could not run**

- It only checked that an element existed, so it listed hidden and blocked actions. With the Edit Account sheet open, it listed 11 page actions that did nothing.
- It now uses the same check that runs the action (`canRunFromCommandDialog`). A sheet with no shortcut targets shows "No results".

**Leftover `keydown-action` binding**

- #17016 removed its last use, but the global binding still swallowed `ArrowDown`. The entry is removed.

**Tests and docs**

- New `tests/navigation/shortcutOverlays.spec.ts`. It stubs the encounter POST, so it creates no data.
- The restricted-user test now checks `Search patients`, which is a top-level link since #17016.
- The Playwright guide no longer expands `Encounters` to reach `Search patients`.

### Behaviour changes

- A shortcut no longer reaches a sheet or page while something is open on top of it. For example, `Shift+Enter` from a picker's **Favorites** tab no longer submits the sheet behind it, and `Enter` does nothing while a menu is open. Shortcuts work again once the picker or menu closes.
- The palette can show fewer items, because it no longer lists actions that wouldn't run.

### Testing

- **New spec, run locally against dev builds:** 4 of 4 pass with this branch merged into `3.1/base` (`5cc7938f4`). On `3.1/base` alone 3 of 4 fail, each on the original bug. The fourth covers palette selections, which already work there. Without the dropdown and menu change, the sheet test fails because the create request goes out.
- **Manually, with write requests blocked:** palette actions with mouse, keyboard and on mobile; `Shift+Enter` and `Enter` in the dispense, Add Charge Items and invoice flows from ENG-1169; alert dialog shortcuts; `Escape` closing only the top layer; `Shift+Enter`, `Shift+ArrowLeft` and `Escape` with a dropdown open; `Enter` and `Escape` with a menu open; keyboard selection in both; `Shift+Enter` in autocompletes and inline comboboxes.
- **With #17041 merged in** (drawer conversion and Base UI 1.9.0): the spec and the dispense warning flow pass. That check ran before this branch's final rebase and before the dropdown and menu change. That change was only checked against the Base UI 1.9.0 source, which keeps the attributes the selector uses.
- **Static checks:** `tsc`, ESLint on the changed files, Prettier and `npm run build` pass.

The full Playwright suite hasn't been run on this branch. The spec ran locally as `care-fac-admin`, and CI uses `admin`. Submenus, context menus and menubars weren't tried in the UI. They use the same popup, which was checked in the source, and the local data has no queue tokens to reach the submenu.

### Notes for review

- `keyboardShortcutUtils.ts` stays compatible for its other caller, `ShortcutContext`. `fromCommandDialog` is optional.
- Menus match on `role='menu'` rather than each popup slot, which covers dropdown, context and menubar menus and their submenus in one line. Select needs its slot because Base UI gives the popup `role="presentation"`.
- Comboboxes stay out of the selector. With the search box in the popup they already have `role="dialog"`. Inline ones keep focus in the text box, so the input guard applies.
- A blocked shortcut still starts the 300ms debounce, which is why the spec waits between presses. That behaviour is unchanged.
- There's no Jira ticket yet, so `validate-jira-ticket` is expected to fail until the title has a key.

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [x] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [x] Add or update Playwright tests for related changes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0eebadfb4123`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.