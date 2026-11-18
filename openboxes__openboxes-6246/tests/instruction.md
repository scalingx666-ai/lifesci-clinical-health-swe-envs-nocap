# Issue

**Title:** #6245 Redirect product/show to the stock card and remove dead phonecat view

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:**

**Description:**

Product links on scaffolded pages (e.g. Products → Components, `/productComponent`) point to `product/show/<id>`. `ProductController.show()` was an empty action that rendered `views/product/show.gsp`, a leftover AngularJS "phonecat" tutorial whose CSS/JS (`js/product/**`, `js/angular/**`) were never committed, under `layouts/main.gsp`, whose `application.css`/`application.js` were removed in OBGM-402. The result was an unstyled, empty page for every product link (HTTP 200, even for ids that do not exist).

This PR:
- makes `ProductController.show()` redirect to `inventoryItem/showStockCard/<id>` (passing only the `id`), so every caller is fixed in one place: the scaffolded `productComponent`, `productPackage` and `productAttributeValue` pages, the hand-written `show.gsp` views that use `g:link controller="product" action="show"`, and bookmarked URLs;
- deletes the dead `grails-app/views/product/show.gsp`;
- adds `ProductControllerShowSpec` (redirect with an id, only the id is forwarded, redirect without an id).

**Access:** unchanged. Neither `product:show` nor `inventoryItem:showStockCard` has an RBAC rule in `runtime.groovy` or `RoleInterceptor`, so the same users can reach both. The stock card already has an Edit button for users who can edit.

**Invalid ids:** `showStockCard` already handles a missing/unknown product by setting a flash message and redirecting to the dashboard (the current React dashboard does not display that message, which is existing behaviour for any unknown stock card id), instead of the previous blank 200.

**Not changed (separate cleanup):** `layouts/main.gsp` (now only used by the superuser-only `quartz/list`) and the many `<asset:stylesheet src="main.css"/>` references to a file that no longer exists.

**Testing:**
- `./gradlew test --tests '*ProductControllerShowSpec' --tests '*RoleInterceptorSpec'` passes (100 tests, 0 failures).
- Manually checked on a running instance built from this branch: all product links on `/productComponent` redirect to the stock card, which renders fully styled with no failing local resources; `/productPackage`, `/productAttributeValue`, `/product/edit/<id>` behave as before; a read-only (BROWSER) user gets the same access as before.

---
### :camera: Screenshots & Recordings (optional)

No screenshots attached. Before: an unstyled, empty page with a bare "Dashboard" link and breadcrumb. After: the regular, fully styled stock card page.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_012eF3ifCakhdS4WtwpUq3V8

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4b43ad8d5561`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.