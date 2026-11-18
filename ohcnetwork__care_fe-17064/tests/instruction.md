# Issue

**Title:** Add encounter type menu and saved default to the facility sidebar (3.1)

## Description

## Proposed Changes

The facility sidebar now has the encounter behaviour from the careui [sidebar-01 block](https://careui.ohc.network/#block-preview-sidebar-01), which we hadn't built.

- The collapsible **Encounters** group becomes an **Encounters & Locations** section. It holds the encounter link and **Search by Location** (`/encounters/locations`).
- The encounter link is labelled with the list on screen (e.g. "Inpatient"). On any other page it shows and opens the user's default list.
- A **⋯** button beside it opens **Encounter Types**: All Encounters plus each enabled class, then **Set Default →**. Set Default switches the same menu to a **Set default encounter** radio list. Choosing one saves it and opens that list.
- With a single enabled encounter class the menu is hidden and only the link shows.
- The facility overview's **Encounters** quick action opens the same default list.

### Where the default is stored

careui keeps the default in browser storage (localStorage). Here it is saved to the user's account through the existing `users/set_preferences` API, under the key `encounter_list.default_class`. Ward computers are often shared, so a per-browser default would carry over between staff. With nothing saved, it falls back to `REACT_DEFAULT_ENCOUNTER_TYPE`, then `all`. `useUserPreferences` gains a small `setPreference(key, value)` for this.

### Implementation notes

- `src/components/ui/sidebar/facility/encounter-nav-item.tsx` renders the item and menu. It uses `DropdownMenu` on mobile too, opening below the button, as `nav-user` and the facility switcher already do.
- `NavigationLink` gains an optional `element` to replace the default menu item while section and visibility rules still apply. `NavLink` and `isNavigationActive` are exported from `nav-main.tsx` for it.
- `/facility/:id/encounters` (typed directly; nothing links to it) still redirects using the env default.

### Testing

- `tsc`, ESLint, Prettier and knip are clean.
- `tests/navigation/sidebarNavigation.spec.ts`: three existing tests updated for the new section, plus a new test. It opens another list from the menu, sets a default and checks that it is saved and still used after a reload. It clears the saved default before and after. All 11 tests pass locally against a production build; the new one also passed 3 repeated runs.
- `tests/organization/patient/helpers.ts` now opens All Encounters through the new menu. The two specs using it couldn't run locally because the dev DB lacks the "Facility with Patients" fixture, so they rely on CI. The changed steps pass on their own against a local facility.
- Manually checked at 1280 px and 375 px: menu placement, Set Default view, navigation, and the mobile drawer closing after a pick.

## Merge Checklist

- [x] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [x] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [x] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [x] Add or update Playwright tests for related changes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e9285a0cbbaa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.