# Issue

**Title:** Fix shortcuts stopping after a completed dispense

## Description

## Proposed Changes

After a completed dispense, encounter shortcuts keep working and the next dispense from the same page goes through.

**The bugs**

All of these start when a dispense completes. They clear on a reload, on leaving the Dispense History tab if the drawer was opened there, or by reopening the drawer and closing it without dispensing.

- Opened with `Shift+D` or Encounter Actions: `Shift+D` and `G` then `N` do nothing, and shortcut hints vanish from Encounter Actions ("Add Allergy A" becomes "Add Allergy"). Changing encounter tab doesn't clear it.
- From any route, the next dispense at the same location fails with "Prescription is not active" and the drawer stays open. Retrying in that drawer fails again; Cancel and starting over works.
- Picking a different location for the next dispense is ignored, and the drawer still shows the old one.
- The next drawer shows the stock from before the dispense.

Closing the drawer without dispensing shows none of this. With auto-invoice on and an open account, closing the invoice sheet clears it.

**The cause**

`onDispenseComplete` in `DispenseButton` closes the drawer but leaves `location` set, unlike the `onOpenChange` close path. `DispenseDrawer` renders only while `location` is set, so it stays mounted while closed and keeps state that was meant to last for one dispense:

- `useShortcutSubContext("patient:search:-global", { ignoreInputFields: true })` stays live. With `Shift+D` or Encounter Actions the drawer renders from `EncounterProvider` beside the page, so this beats `encounter` from `EncounterShow`.
- `alternateIdentifier` is created once, on mount. The next dispense sends the same value, the backend finds the order that was just completed and rejects it.
- `currentLocation` is also set once, on mount, so a new `selectedLocation` is ignored.
- The inventory it loaded stays too, so the next drawer shows old stock.

**The fix**

- `onDispenseComplete` now clears `location`, so the drawer unmounts the same way it does on Cancel.
- `resetInvoiceState` no longer clears it. By then it's already cleared, and `CreateInvoiceSheet` never read it.

Tying the drawer's shortcut settings to `open` isn't enough. That would fix the shortcuts, but the second dispense and the location pick would stay broken.

### Behaviour changes

- After a dispense the drawer goes at once, as it does on Cancel, instead of sliding out over about 450 ms.
- The location picker no longer shows "Current Location" after a dispense, which also matches Cancel.

### Testing

Real keystrokes in Chromium on production builds of `3.1/base` at `e9285a0cb`, which includes #17041 and #17062, with and without this branch merged, at 865×934 and 1440×900, against a plugin-free backend on a copy of the DB. Every dispense that went through sent `POST batch_requests/` and `PUT order/dispense/…/`.

| Check | `3.1/base` | This branch |
| --- | --- | --- |
| `Shift+D` after a dispense opened with `Shift+D` or Encounter Actions | does nothing, 4 of 4 | opens the picker, 4 of 4 |
| Encounter Actions hints after that dispense | gone, 4 of 4 | still there, 4 of 4 |
| Shortcut state on the provider after that dispense | `patient:search:-global`, `ignoreInputFields: true` | `encounter`, `ignoreInputFields: false` |
| `Shift+D` right after the drawer closes, no click first | does nothing, 2 of 2 | opens the picker, 2 of 2 |
| `G` then `N` after a dispense at 1440 | stays on `/medicines`, 2 of 2 | goes to `/notes`, 2 of 2 |
| Second dispense at the same location, from `Shift+D`, Encounter Actions and the History tab | 400 "Prescription is not active", drawer stays open, 6 of 6 | goes through, 6 of 6 |
| Stock shown in the next drawer | stale, 2 of 2 | matches the backend, 2 of 2 |
| Picking another location for the next dispense | drawer still shows Pharmacy | drawer shows Bio-Chemistry Lab |
| Escape or Cancel without dispensing | shortcuts back, 8 of 8 | shortcuts back, 8 of 8 |
| `Shift+Enter` from the quantity input, from `Shift+D` and the History tab | dispensed, 4 of 4 | dispensed, 4 of 4 |
| `ignoreInputFields` after a dispense from the History tab | stays `true`, 4 of 4 | `false`, 4 of 4 |
| Typing "para" in Add Item and dispensing, from all three routes | dispensed, 6 of 6 | dispensed, 6 of 6 |
| Two medicines, one with quantity 2 | stock drops by 2 and 1, 2 of 2 | stock drops by 2 and 1, 2 of 2 |
| Server refuses the dispense | drawer and item stay, retry works, 2 of 2 | drawer and item stay, retry works, 2 of 2 |
| Changing location inside the drawer, then dispensing | dispenses from the new location, 2 of 2 | dispenses from the new location, 2 of 2 |
| Auto-invoice on: sheet opens with the item, Cancel, second dispense, Create Invoice | passes, 4 of 4 | passes, 4 of 4 |
| Auto-invoice on, no open account | shortcuts stay dead | shortcuts work |
| Status `PUT` held for 3 seconds while the drawer unmounts | not run | completes, order is `completed` |
| Touch emulation at 390×844, two dispenses from the History tab | second gets the 400, 2 of 2 | both go through, 2 of 2 |

- The build passes on this merge, and `tsc` passes on this branch at `a8ae033c3`.
- This branch merges into `e9285a0cb` with no conflicts.

**Found while testing, not fixed here**

All three happen on `3.1/base` too:

- After a dispense from the History tab the new order isn't listed. `onDispenseComplete` invalidates `dispenseOrders`, but the list's key has been `infinite-dispenseOrders` since #16554.
- Opening the drawer from the History tab before its list has loaded loses the drawer when the list arrives, because `DispenseHistory` renders `DispenseButton` at a different place in each loading state.
- `alternate_identifier` is the encounter plus a millisecond timestamp. Two sessions opening the drawer in the same millisecond on the same patient and location share one, so the second gets "Prescription is not active" on its first dispense. I only saw this with parallel test runs.

**Not tested**

- Firefox, Safari and real phones. The 390×844 runs emulate touch.
- The Playwright suite on this merge. CI on `a8ae033c3`, before #17041, failed only `valuesetCreate.spec.ts:144`, which fails across 3.1.
- A build made with `REACT_ENABLE_AUTO_INVOICE_AFTER_DISPENSE`. The auto-invoice runs flipped that flag in a copy of each production build, so the rest of the code matches the builds above.

No spec was added or changed, because nothing in `tests/` covers Dispense.

There's no Jira ticket, so `validate-jira-ticket` is expected to fail until the title has a key.

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `01d570b2e868`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.