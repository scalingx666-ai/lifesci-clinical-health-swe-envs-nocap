# Issue

**Title:** Fix letters being swallowed in the Dispense Add Item search

## Description

## Proposed Changes

Keys typed into the Dispense **Add Item** search now stay in the box, so the medicine picker can be searched again.

**The bug**

When Dispense is opened from an encounter's **Dispense History** tab, the Add Item search silently loses keys. Typing "para" leaves it empty, so no search is sent. The keys lost are:

- Lowercase, or capitals with Caps Lock: `a d e f g h k l m p r s`. `h` only gets through when it comes straight after `g`.
- With Shift held: `D E F U` and the symbols on 1 to 9.

Opening Dispense with the `Shift+D` shortcut doesn't show the bug.

The note dialog in `ProcessSpecimen` sets the same flag and has the same bug, losing `c e m p r s t`.

**The cause**

- `DispenseDrawer` sets `ignoreInputFields: true` so `Shift+Enter` works from its fields, but that lets every shortcut run from inside inputs.
- From the Dispense History tab the active sub-context stays `encounter`, so the encounter and global single-letter shortcuts are live. With `Shift+D` the drawer renders from `EncounterProvider` and the sub-context is `patient:search:-global`, which has none.
- The overlay guard in `useKeyboardShortcuts.ts` skips encounter shortcuts while a sheet or dialog is open, but it looks for `data-state="open"`. #17008 moved `sheet.tsx` and `dialog.tsx` from Radix to Base UI, which sets `data-open`, so the guard no longer matches.

This is a 3.1 regression from #17008: typing works on `develop` and on `a53aab7260^`, and is broken at `a53aab7260` and on `3.1/base`.

**The fix**

- A printable key without Ctrl, Cmd or Alt now always stays in the field, even with `ignoreInputFields` on. Enter, Escape, arrow keys and Cmd/Ctrl combinations behave as before.
- `DispenseDrawer` keeps `ignoreInputFields`, because `Shift+Enter` still needs it.
- The `data-state` guard is unchanged. Reviving it would change which shortcuts work in overlays, and that hasn't been tested.

### Behaviour changes

- `Shift+?` inside a field in the Dispense drawer, the `ProcessSpecimen` note dialog or the patient search page no longer opens the page actions palette. `PatientIndex.tsx` turns on `ignoreInputFields` as well. Text fields now type `?`. The patient search phone field does nothing, and it takes focus on load, so you have to leave the field first. Outside a field `Shift+?` still opens the palette.

### Testing

Real keystrokes in Chromium on production builds of `87b75d628` with and without this change, against a plugin-free backend on a copy of the DB.

| Check | `3.1/base` | This branch |
| --- | --- | --- |
| "para" from the Dispense History tab at 390×844 touch | empty, 21 of 21 | `para`, Paracetamol listed and added, 24 of 24 |
| "para" at 1280×720 | empty | `para`, Paracetamol listed and added |
| The alphabet in one go | `bchijnoqtuvwxyz` | all 26 |
| Each letter alone | 12 lost | none lost |
| `PARACETAMOL?` with no Shift key | `CTO?` | all of it |
| A to Z with Shift held | `D E F U` lost | all 26 |
| `Shift+1` to `Shift+0` | only `)` | all 10 |
| The same typing checks from `Shift+D` | nothing lost | nothing lost |
| `Shift+Enter` from the quantity input | dispensed, 2 of 2 | dispensed, 4 of 4 |
| `a`, `g m` and `Shift+?` outside a field | work | work |
| `Cmd+K` inside the drawer's search box | reaches the hook, 3 of 3 on each route | reaches the hook, 3 of 3 on each route |
| `Cmd+K` and `Ctrl+K` from a plain input on the users page | focus the search box | focus the search box |
| `Escape` in the search box | closes the picker only | closes the picker only |
| `ProcessSpecimen` note dialog, "para" | `aa` | `para` |
| `ProcessSpecimen` note dialog, each letter alone | 7 lost | none lost |
| `tests/navigation/shortcutOverlays.spec.ts` | 4 of 4 | 4 of 4 |

- The `Shift+Enter` runs on this branch were the Dispense History tab twice at 1280×720, `Shift+D` once and the touch viewport once. Each sent `POST batch_requests/` and `PUT order/dispense/…/`, then closed the drawer.
- `tsc`, ESLint and Prettier on the changed file, and `npm run build`, pass.
- `3.1/base` then moved to `9511ad321`, which reworked the encounter page, so I repeated the typing, search, `Shift+Enter`, shortcut, `ProcessSpecimen` and spec checks on this branch merged into it, against that base alone. The results were the same.

**Not tested**

- Real phones or on-screen keyboards. The 390×844 runs emulate touch but send hardware-style key events.
- Firefox and Safari.
- The full Playwright suite. Only the shortcut spec ran.
- Saving a `ProcessSpecimen` note. The dialog was tested on a real collected specimen, then cancelled.
- `ProcessSpecimen` on `develop`. The guard only covers `encounter` shortcuts, so that dialog may have lost letters before #17008 too.

No spec was added or changed. `shortcutOverlays.spec.ts` passes with and without this fix, and no existing test types into a field with `ignoreInputFields` on.

There's no Jira ticket yet, so `validate-jira-ticket` is expected to fail until the title has a key.

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `01f5480cb6c6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.