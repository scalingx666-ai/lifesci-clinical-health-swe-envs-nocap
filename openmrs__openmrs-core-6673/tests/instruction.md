# Issue

**Title:** TRUNK-6824: Request paths with a repeated slash fail with 500 on core 3.0

## Description

## Description of what I changed

On core master, `GET /openmrs//ws/rest/v1/session` answers 500:

```
IllegalArgumentException: Invalid contextPath '/openmrs/ws': must match the start of requestPath: '/openmrs//ws/rest/v1/session'
    at org.springframework.web.util.ServletRequestPathUtils.parseAndCache(ServletRequestPathUtils.java:70)
    at org.springframework.web.filter.ServletRequestPathFilter.doFilter(ServletRequestPathFilter.java:50)
    at org.springframework.security.config.annotation.web.configuration.WebSecurityConfiguration$CompositeFilterChainProxy.doFilter(WebSecurityConfiguration.java:317)
    at org.openmrs.web.security.RefreshableDelegatingFilterProxy.doFilter(RefreshableDelegatingFilterProxy.java:84)
```

Tomcat normalizes the servlet path and path info, but `getRequestURI()` keeps the slashes the client sent. Spring Security's composite runs `ServletRequestPathFilter` ahead of `FilterChainProxy`, and its parse needs the context path plus the servlet path to start that URI. So a repeated slash at or before `/ws` fails there with a 500, before the firewall can answer the 400 it gives a `//` further in. The O3 patient chart's visit history requests `/openmrs//ws/rest/v1/visit`, which 2.x served, so the Visits dashboard shows "Error 500" on a 3.0 backend.

`RepeatedSlashFilter`, mapped right after `charsetFilter` in `web.xml`, collapses each run of slashes in the request URI, URL and context path. Everything downstream (Spring's path parsing, `springSecurityFilterChain`, `ModuleFilter`, CSRFGuard and `OpenmrsAuthorizationFilter`) then sees the path the container dispatched on. Requests without `//` pass through unwrapped.

`WebSecurityConfig`'s javadoc keeps `StrictHttpFirewall` at its defaults because a URL rule matches the request URI rather than the dispatched path. After this filter the two agree about repeated slashes, so `//admin/x` is still challenged by an `/admin/**` rule. The firewall settings are unchanged, and `filterChain_shouldRejectAUrlShapeThatCouldWalkAroundAUrlRule`, which sends `//` to the chain directly, still expects 400. The filter changes nothing but repeated slashes. `/openmrs/ws;x=y/rest/v1/session` and `/openmrs/x/../ws/rest/v1/session` still fail with a 500 in `ServletRequestPathFilter`, as on master, and Tomcat itself refuses an encoded slash with 400.

Tests:
- `RepeatedSlashFilterTest` covers the URI, URL and context path shapes Tomcat produces, and leaves the query string and `%2F` alone. It also shows `ServletRequestPathUtils.parseAndCache` failing on the raw request and succeeding on the filtered one.
- `WebSecurityConfigIntegrationTest` runs the filter ahead of the real chain. Guarded URLs reached through `//` (including `/openmrs//ws/admin/x`) get 401, and public ones get 200. Without the filter these get 400 from the firewall, or, where the repeated slash sits at or before the `/ws` servlet path, the `ServletRequestPathFilter` exception.
- `WebXmlTest` (webapp module) reads `web.xml` and requires a `RepeatedSlashFilter` mapping on `/*` for requests, ahead of `springSecurityFilterChain`'s. It fails if those lines are deleted, moved below the security chain, or narrowed.

Checked by hand on Tomcat 11 with this war and the RefApp module set on 3.0:

| Request | master | this branch |
| --- | --- | --- |
| `/openmrs//ws/rest/v1/session`, `//openmrs/ws/...`, `/openmrs///ws/...` | 500 | 200 |
| `/openmrs/ws//rest/v1/session`, `/openmrs//login.htm` | 400 | 200 |
| The O3 visit-history URL above | 500 | 200, same body as with one slash |
| Anonymous `//ws/fhir2/R4/Patient`, `//admin/index.htm`, token-less POST to `//admin/users/user.form` | not measured | 401, 302 to login, 302 to `error.html` (same as with one slash) |
| `/openmrs/ws/rest/v1/%2F%2Fsession` | 400 | 400 |

The RefApp 3.7.1 Visits dashboard lists the patient's visits again instead of "Error 500".

A trailing `//` now collapses to a single trailing slash. Core 3.0 answers that with a 500 whether or not this change is in (`/openmrs/ws/rest/v1/session/` does as well), where the firewall used to give 400.

Left as they are, both minor:
- SonarCloud's java:S3398: `collapse` could move into `CollapsedSlashesRequest`.
- `AuthorizedUrlMatcher`'s javadoc still says a rule matches the raw request URI. Repeated slashes are now collapsed before any rule matches, and the conclusion it draws (name the `/ws` twin and the module prefixes) still holds.

## Issue I worked on

see https://issues.openmrs.org/browse/TRUNK-6824

## Checklist: I completed these to help reviewers :)

- [x] My IDE is configured to follow the [**code style**](https://wiki.openmrs.org/display/docs/Java+Conventions) of this project.

- [x] I have **added tests** to cover my changes.

- [x] I ran `./mvnw clean package` right before creating this pull request and added all formatting changes to my commit.

- [x] All new and existing **tests passed**.

- [x] My pull request is **based on the latest changes** of the master branch.

`mvn clean verify` from the root, on this head: all 13 modules pass, with 0 failures and 0 errors (api 5604 tests, web 324, webapp 1). Spotless changed nothing.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01WMHrjRkMgotZngQzt31zSK

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a69b14a84bf9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.