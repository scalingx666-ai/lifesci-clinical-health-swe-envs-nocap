# Issue

**Title:** Bump requests from 2.31.0 to 2.32.0 in the pip group across 1 directory

## Description

Bumps the pip group with 1 update in the / directory: [requests](https://github.com/psf/requests).

Updates `requests` from 2.31.0 to 2.32.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/psf/requests/releases">requests's releases</a>.</em></p>
<blockquote>
<h2>v2.32.0</h2>
<h2>2.32.0 (2024-05-20)</h2>
<h2>🐍 PYCON US 2024 EDITION 🐍</h2>
<p><strong>Security</strong></p>
<ul>
<li>Fixed an issue where setting <code>verify=False</code> on the first request from a
Session will cause subsequent requests to the <em>same origin</em> to also ignore
cert verification, regardless of the value of <code>verify</code>.
(<a href="https://github.com/psf/requests/security/advisories/GHSA-9wx4-h78v-vm56">https://github.com/psf/requests/security/advisories/GHSA-9wx4-h78v-vm56</a>)</li>
</ul>
<p><strong>Improvements</strong></p>
<ul>
<li><code>verify=True</code> now reuses a global SSLContext which should improve
request time variance between first and subsequent requests. It should
also minimize certificate load time on Windows systems when using a Python
version built with OpenSSL 3.x. (<a href="">#6667</a>)</li>
<li>Requests now supports optional use of character detection
(<code>chardet</code> or <code>charset_normalizer</code>) when repackaged or vendored.
This enables <code>pip</code> and other projects to minimize their vendoring
surface area. The <code>Response.text()</code> and <code>apparent_encoding</code> APIs
will default to <code>utf-8</code> if neither library is present. (<a href="">#6702</a>)</li>
</ul>
<p><strong>Bugfixes</strong></p>
<ul>
<li>Fixed bug in length detection where emoji length was incorrectly
calculated in the request content-length. (<a href="">#6589</a>)</li>
<li>Fixed deserialization bug in JSONDecodeError. (<a href="">#6629</a>)</li>
<li>Fixed bug where an extra leading <code>/</code> (path separator) could lead
urllib3 to unnecessarily reparse the request URI. (<a href="">#6644</a>)</li>
</ul>
<p><strong>Deprecations</strong></p>
<ul>
<li>Requests has officially added support for CPython 3.12 (<a href="">#6503</a>)</li>
<li>Requests has officially added support for PyPy 3.9 and 3.10 (<a href="">#6641</a>)</li>
<li>Requests has officially dropped support for CPython 3.7 (<a href="">#6642</a>)</li>
<li>Requests has officially dropped support for PyPy 3.7 and 3.8 (<a href="">#6641</a>)</li>
</ul>
<p><strong>Documentation</strong></p>
<ul>
<li>Various typo fixes and doc improvements.</li>
</ul>
<p><strong>Packaging</strong></p>
<ul>
<li>Requests has started adopting some modern packaging practices.
The source files for the projects (formerly <code>requests</code>) is now located
in <code>src/requests</code> in the Requests sdist. (<a href="">#6506</a>)</li>
<li>Starting in Requests 2.33.0, Requests will migrate to a PEP 517 build system
using <code>hatchling</code>. This should not impact the average user, but extremely old
versions of packaging utilities may have issues with the new packaging format.</li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/matthewarmand"><code>@​matthewarmand</code></a> made their first contribution in <a href="">psf/requests#6258</a></li>
<li><a href="https://github.com/cpzt"><code>@​cpzt</code></a> made their first contribution in <a href="">psf/requests#6456</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/psf/requests/blob/main/HISTORY.md">requests's changelog</a>.</em></p>
<blockquote>
<h2>2.32.0 (2024-05-20)</h2>
<p><strong>Security</strong></p>
<ul>
<li>Fixed an issue where setting <code>verify=False</code> on the first request from a
Session will cause subsequent requests to the <em>same origin</em> to also ignore
cert verification, regardless of the value of <code>verify</code>.
(<a href="https://github.com/psf/requests/security/advisories/GHSA-9wx4-h78v-vm56">https://github.com/psf/requests/security/advisories/GHSA-9wx4-h78v-vm56</a>)</li>
</ul>
<p><strong>Improvements</strong></p>
<ul>
<li><code>verify=True</code> now reuses a global SSLContext which should improve
request time variance between first and subsequent requests. It should
also minimize certificate load time on Windows systems when using a Python
version built with OpenSSL 3.x. (<a href="">#6667</a>)</li>
<li>Requests now supports optional use of character detection
(<code>chardet</code> or <code>charset_normalizer</code>) when repackaged or vendored.
This enables <code>pip</code> and other projects to minimize their vendoring
surface area. The <code>Response.text()</code> and <code>apparent_encoding</code> APIs
will default to <code>utf-8</code> if neither library is present. (<a href="">#6702</a>)</li>
</ul>
<p><strong>Bugfixes</strong></p>
<ul>
<li>Fixed bug in length detection where emoji length was incorrectly
calculated in the request content-length. (<a href="">#6589</a>)</li>
<li>Fixed deserialization bug in JSONDecodeError. (<a href="">#6629</a>)</li>
<li>Fixed bug where an extra leading <code>/</code> (path separator) could lead
urllib3 to unnecessarily reparse the request URI. (<a href="">#6644</a>)</li>
</ul>
<p><strong>Deprecations</strong></p>
<ul>
<li>Requests has officially added support for CPython 3.12 (<a href="">#6503</a>)</li>
<li>Requests has officially added support for PyPy 3.9 and 3.10 (<a href="">#6641</a>)</li>
<li>Requests has officially dropped support for CPython 3.7 (<a href="">#6642</a>)</li>
<li>Requests has officially dropped support for PyPy 3.7 and 3.8 (<a href="">#6641</a>)</li>
</ul>
<p><strong>Documentation</strong></p>
<ul>
<li>Various typo fixes and doc improvements.</li>
</ul>
<p><strong>Packaging</strong></p>
<ul>
<li>Requests has started adopting some modern packaging practices.
The source files for the projects (formerly <code>requests</code>) is now located
in <code>src/requests</code> in the Requests sdist. (<a href="">#6506</a>)</li>
<li>Starting in Requests 2.33.0, Requests will migrate to a PEP 517 build system
using <code>hatchling</code>. This should not impact the average user, but extremely old
versions of packaging utilities may have issues with the new packaging format.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>d6ebc4a</code></a> v2.32.0</li>
<li><a href=""><code>9a40d12</code></a> Avoid reloading root certificates to improve concurrent performance (<a href="">#6667</a>)</li>
<li><a href=""><code>0c030f7</code></a> Merge pull request <a href="">#6702</a> from nateprewitt/no_char_detection</li>
<li><a href=""><code>555b870</code></a> Allow character detection dependencies to be optional in post-packaging steps</li>
<li><a href=""><code>d6dded3</code></a> Merge pull request <a href="">#6700</a> from franekmagiera/update-redirect-to-invalid-uri-test</li>
<li><a href=""><code>bf24b7d</code></a> Use an invalid URI that will not cause httpbin to throw 500</li>
<li><a href=""><code>2d5f547</code></a> Pin 3.8 and 3.9 runners back to macos-13 (<a href="">#6688</a>)</li>
<li><a href=""><code>f1bb07d</code></a> Merge pull request <a href="">#6687</a> from psf/dependabot/github_actions/github/codeql-act...</li>
<li><a href=""><code>60047ad</code></a> Bump github/codeql-action from 3.24.0 to 3.25.0</li>
<li><a href=""><code>31ebb81</code></a> Merge pull request <a href="">#6682</a> from frenzymadness/pytest8</li>
<li>Additional commits viewable in <a href="https://github.com/psf/requests/compare/v2.31.0...v2.32.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=requests&package-manager=pip&previous-version=2.31.0&new-version=2.32.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

Dependabot will resolve any conflicts with this PR as long as you don't alter it yourself. You can also trigger a rebase manually by commenting `@dependabot rebase`.

[//]: # (dependabot-automerge-start)
[//]: # (dependabot-automerge-end)

---

<details>
<summary>Dependabot commands and options</summary>
<br />

You can trigger Dependabot actions by commenting on this PR:
- `@dependabot rebase` will rebase this PR
- `@dependabot recreate` will recreate this PR, overwriting any edits that have been made to it
- `@dependabot merge` will merge this PR after your CI passes on it
- `@dependabot squash and merge` will squash and merge this PR after your CI passes on it
- `@dependabot cancel merge` will cancel a previously requested merge and block automerging
- `@dependabot reopen` will reopen this PR if it is closed
- `@dependabot close` will close this PR and stop Dependabot recreating it. You can achieve the same result by closing it manually
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore <dependency name> major version` will close this group update PR and stop Dependabot creating any more for the specific dependency's major version (unless you unignore this specific dependency's major version or upgrade to it yourself)
- `@dependabot ignore <dependency name> minor version` will close this group update PR and stop Dependabot creating any more for the specific dependency's minor version (unless you unignore this specific dependency's minor version or upgrade to it yourself)
- `@dependabot ignore <dependency name>` will close this group update PR and stop Dependabot creating any more for the specific dependency (unless you unignore this specific dependency or upgrade to it yourself)
- `@dependabot unignore <dependency name>` will remove all of the ignore conditions of the specified dependency
- `@dependabot unignore <dependency name> <ignore condition>` will remove the ignore condition of the specified dependency and ignore conditions
You can disable automated security fix PRs for this repo from the [Security Alerts page](https://github.com/google/android-fhir/network/alerts).

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c6adeb424aae`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.