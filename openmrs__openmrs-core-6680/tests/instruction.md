# Issue

**Title:** TRUNK-6826: Request paths with a trailing slash find no handler on core 3.0

## Description

## Description of what I changed

On core 3.0, `/openmrs/ws/rest/v1/session/` no longer reaches the handler for `/openmrs/ws/rest/v1/session`. A 2.x server (platform 2.9.0-SNAPSHOT, Spring 5.3.30) answers both with 200. Spring 7 has no option to match a handler mapping to a path with a trailing slash; in spring-webmvc/spring-web 7.0.9, `PathMatchConfigurer`, `RequestMappingHandlerMapping` and `PathPatternParser` have no trailing-slash member, while 6.2.12's `PathPatternParser` still has `setMatchOptionalTrailingSeparator`.

With the RefApp module set the missing handler shows up as a 500 rather than a 404: webservices.rest maps `/rest/**` to `unknownResourceController` through a `SimpleUrlHandlerMapping`, and no handler adapter supports that `@Controller` (`ServletException: No adapter for handler [...UnknownResourceController...]`). `/ws/rest/nosuch` answers the same 500 without any trailing slash, so that part belongs to the REST module and is not changed here.

`TrailingSlashFilter` hands a `/ws` request whose path ends in `/` to Spring's `UrlHandlerFilter`, which trims the slash from the request URI, URL and path info. It passes on unchanged:
- requests the container mapped to any other servlet,
- `/openmrs/ws/` itself, where legacyui serves its index page (`UrlHandlerFilter` leaves the servlet root alone),
- a request URI that does not start with the context path and `/ws/`, such as `/openmrs//ws/x/`, which `UrlHandlerFilter` cannot parse,
- a request URI ending in `//`. `UrlHandlerFilter` trims one slash, which would leave the URI ending in a single `/` that the firewall no longer rejects. Passed on unchanged, it gets the firewall's 400, as on master.

`web.xml` maps it right after `charsetFilter`, ahead of `springSecurityFilterChain` as `UrlHandlerFilter`'s javadoc asks, and so ahead of `openmrsAuthorizationFilter`. An `AuthorizedUrlMatcher` rule therefore judges the path the handler is chosen on: an exact rule on `/secure/x` still challenges `/ws/secure/x/`.

Tests:
- `TrailingSlashFilterTest`: URI, URL and path info trimmed with the query string kept, in a `/openmrs` and a root deployment; requests left alone without a trailing slash, at the `/ws` root, without path info, to another servlet, with `//` after the context path, with a URI ending in `//`, and with a dot segment that the container mapped to `/scripts`.
- `WebSecurityConfigIntegrationTest`: with the filter ahead of the real `springSecurityFilterChain` and `openmrsAuthorizationFilter`, `/openmrs/ws/public/x/` reaches the `/public/x` handler (404 without the filter), an anonymous `/openmrs/ws/secure/x/` gets 401 from the exact `/secure/x` rule (200 if the filter runs after `openmrsAuthorizationFilter`), and `/openmrs/ws/public/x//`, shaped the way Tomcat delivers it, gets the firewall's 400 (404 without the `//` check).

Checked under `jetty:run` with all 31 O3 modules on a fresh MySQL database, master at ee18bf341b and this branch at its head:

| Request | master | this branch |
| --- | --- | --- |
| `/ws/rest/v1/session/`, `/ws/rest/v1/location/`, `/ws/rest/v1/location/?v=full` | 500 | 200, same as without the slash |
| `/ws/rest/v1/patient/` | 500 | 400, same as without the slash |
| `/ws/rest/v1/nosuchthing/` | 500 | 404 from REST, same as without the slash |
| `/ws/index.htm/` | 404 | 200, same as without the slash |
| POST to `/ws/rest/v1/location/` | not measured | 201 |
| `/ws/fhir2/R4/metadata/`, `/ws/fhir2/R4/Patient/` | 200 | 200, same as without the slash |
| `/ws/` | 200 (legacyui index) | 200 (legacyui index) |
| anonymous `/ws/admin/index.htm/` | not measured | 302 to login, same as without the slash |

Jetty answers any URI with `//` with 400 before the application sees it, so the `//` cases were not run on a server.

If #6673 (TRUNK-6824) also merges, both PRs add a filter at the same place in `web.xml`, and `RepeatedSlashFilter` has to come first. In the other order, on Tomcat, `/openmrs//ws/rest/v1/session/` and `/openmrs/ws/rest/v1/session//` still find no handler.

Seen while checking, left as they are:
- An anonymous GET of `/ws/fhir2/R4/metadata/` now answers 200 instead of 401, the same as `/ws/fhir2/R4/metadata`, because fhir2's `endsWith("/metadata")` check now sees the trimmed URI.
- Multipart POSTs to `/ws/rest/v1/...` answer 500 with or without the slash: `ClassCastException` in legacyui's `XSSFilter` (`StrictHttpFirewall$StrictFirewalledRequest` is not a `MultipartHttpServletRequest`).
- Anonymous `GET /ws/rest/v1/location` answers 500 (`AuthorizationDeniedException`, "Privileges required: Get Locations") with or without the slash.

## Issue I worked on

see https://issues.openmrs.org/browse/TRUNK-6826

## Checklist: I completed these to help reviewers :)

- [x] My IDE is configured to follow the [**code style**](https://wiki.openmrs.org/display/docs/Java+Conventions) of this project.

- [x] I have **added tests** to cover my changes.

- [x] I ran `./mvnw clean package` right before creating this pull request and added all formatting changes to my commit.

- [x] All new and existing **tests passed**.

- [x] My pull request is **based on the latest changes** of the master branch.

`mvn clean install` from the root on this head: all 13 modules pass, with 0 failures and 0 errors (api 5604 tests, web 321).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7ad155e529e4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.