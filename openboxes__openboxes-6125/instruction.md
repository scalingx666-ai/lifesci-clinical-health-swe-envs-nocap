# Issue

**Title:** Apply the unified design theme to legacy GSP pages in 3 files

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:** relates to #6070, and takes the stylesheet from #6073

**Description:**

This lands the legacy-page half of #6073 in three files, by linking that PR's stylesheet directly from `custom.gsp` instead of routing it through a new layout.

`openboxes-theme.css` comes from #6073 (by @christianallen) — it is the file that carries the entire design. It is unchanged apart from a provenance note in its header and one fix from review here (the `.box` scroll rule is now gated on `@supports selector(:has(*))`; see the thread on that rule). Both deviations are called out in the file header so the two copies can be reconciled later.

#### Why it can be this small

#6073 ships the stylesheet by adding `layouts/default.gsp` — a themed twin of `custom.gsp` — and a `GroovyPageLayoutFinder` subclass, a `BeanFactoryPostProcessor` and a `LayoutInterceptor` so SiteMesh resolves pages that declared `custom` to `default` instead.

Diffed against `custom.gsp`, that 760-line layout differs by **nine lines** — the favicon, the theme stylesheet, and a script block:

```
- link rel="shortcut icon" href="${resource(dir:'images',file:'favicon.ico')}"
+ link rel="shortcut icon" href="${request.contextPath}/static/images/favicon-unified.ico?v=1"

+ (comment) Uniform design theme: must load after layoutHead ...
+ link rel="stylesheet" href="${resource(dir:'css',file:'openboxes-theme.css')}?v=${g.meta(name: 'app.version')}"

- script type="text/javascript"
-     $.notify.defaults({ autoHideDelay: ... });
- /script
```

(angle brackets omitted above — GitHub strips them from PR bodies; `git diff` the two files to see it verbatim)

Only one of those lines carries the design. A `g:if` tag around that stylesheet link in `custom.gsp` reaches the same end state, so the second layout, the finder, the post-processor, the interceptor and the ~665 lines of tests pinning them are not needed.

#### What is in this PR

| File | Lines | |
|---|---|---|
| `src/main/webapp/css/openboxes-theme.css` | +3,479 | from #6073, plus a provenance header and the `:has()` gate |
| `grails-app/views/layouts/custom.gsp` | +10 | the flag check and the stylesheet link |
| `grails-app/conf/application.yml` | +6 | `openboxes.layout.unified.enabled`, documented |

The stylesheet is self-contained: every asset inside it is an inline SVG data URI, and it references none of the markup classes #6073 adds. So none of the 254 page GSPs change, and no image files come with it. Its `:root` block is the current token set from `src/css/colors.scss`, and it loads after `openboxes.css`, so it also supersedes the older partial copy of those tokens that file carries.

The link sits after the `g:layoutHead` tag so it overrides page-specific CSS, and before `/common/customCss` so per-warehouse header colours keep precedence — the placement the stylesheet's own header documents.

#### The flag

Same config key as #6073, `openboxes.layout.unified.enabled`, so an instance that has already set it keeps its meaning. **Defaulted to `true` here** rather than `false`, so the legacy pages match the React pages out of the box; instances that want the original design set it to `false` in their external config and restart.

The predicate is:

```groovy
!(grailsApplication.config.openboxes.layout.unified.enabled?.toString()?.trim()?.equalsIgnoreCase('false'))
```

The string handling is load-bearing. External `openboxes-config.properties` overrides arrive as strings, so a plain truthiness test — the idiom used elsewhere in this layout — would evaluate `"false"` as true and the opt-out would silently fail. Compared trimmed and case-insensitively so `"FALSE"`, `"False"` and padded values work too. Verified against Boolean `true`/`false`, those string forms, `null`, an empty config branch, and an empty value.

#### Backing it out

A concern raised on #6073 was that a change this size is all-or-nothing to revert. Here the flag is the answer, and it is finer-grained than commit history would be: set `openboxes.layout.unified.enabled = false` in an instance's external config and restart. No code change, no rebuild, no deploy — and it can be done per instance, so one site can drop back to the original design without affecting anyone else.

Backing it out of the branch entirely is a small revert. The stylesheet is purely additive and gated, so nothing else in the tree depends on it.

#### Scope

Legacy desktop GSP pages only. #6073's mobile stylesheet, its React footer and dashboard icon changes, and the bug fixes it found while testing are all still worth landing and are not duplicated here.

#### Base branch and lifetime

This targets `feature/obaf-integration` deliberately, and is intended to stay there rather than move on to `develop`. The expectation is that the legacy GSP pages will largely be converted before OBAF is ready to merge, so this is a stopgap that keeps the two UIs consistent in the meantime — scoped so that it costs little if it is eventually thrown away, and leaves `develop` untouched either way.

---
### :camera: Screenshots & Recordings (optional)

The rendered result is the same as #6073 with its flag on, because it is the same stylesheet. Its screenshots therefore apply unchanged — reproduced here for convenience:

**Order list (legacy GSP) — before:**

![Order list before](https://raw.githubusercontent.com/christianallen/openboxes/issue-assets/desktop-order-list-before.png)

**Order list (legacy GSP) — after:**

![Order list after](https://raw.githubusercontent.com/christianallen/openboxes/issue-assets/desktop-order-list-after.png)

**The React design being matched (`/product/list`):**

![React reference](https://raw.githubusercontent.com/christianallen/openboxes/issue-assets/react-product-list-reference.png)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01SJMs8obK4EorsJQrfeCm7Y

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `61ba6a0b51a6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.