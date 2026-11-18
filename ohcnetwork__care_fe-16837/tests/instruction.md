# Issue

**Title:** Complete tag color integration across remaining tag renderings

## Description

<!-- entire-trail-link-start -->
https://entire.io/gh/ohcnetwork/care_fe/trails/26
<!-- entire-trail-link-end -->

## Proposed Changes

Tag colors are configured in Tag Config settings, but several views still rendered tags as plain `<Badge>` elements, ignoring the assigned color.

- **Switched remaining plain badges to the color-aware `TagBadge`:**
  - `AppointmentDetail` tags section — also drops the manual `parent: ` string prefix in favour of `hierarchyDisplay`
  - `AppointmentsPage` appointment cards
  - `AccountShow` (billing)
  - `RequestOrderShow` / `DeliveryOrderShow` (external supply)

  ```diff
  - <Badge key={tag.id} variant="secondary" className="text-xs">
  -   {tag.display}
  - </Badge>
  + <TagBadge key={tag.id} tag={tag} className="text-xs" />
  ```

- **Surface the color where it is managed:** added a `TagColorDot` swatch to the Admin Tag Config list cards, table rows, and the tag detail header.

- Other tag render sites (patient/encounter cards, locations, activity & charge item definitions, prints, filter selectors) already used `TagBadge`/`TagColorDot` and are untouched.

Not addressed: the parent-tag link in `TagConfigView` still renders without a swatch — the API's parent payload (`TagConfigBase`) carries no `metadata`, so no color is available client-side. Worth a backend follow-up if we want hierarchy colors everywhere.

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

<!-- START COPILOT CODING AGENT SUFFIX -->

-

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9a6e36aeed97`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.