# Issue

**Title:** Bump urllib3 from 2.2.1 to 2.2.2 in the pip group across 1 directory

## Description

Bumps the pip group with 1 update in the / directory: [urllib3](https://github.com/urllib3/urllib3).

Updates `urllib3` from 2.2.1 to 2.2.2
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/urllib3/urllib3/releases">urllib3's releases</a>.</em></p>
<blockquote>
<h2>2.2.2</h2>
<h2>🚀 urllib3 is fundraising for HTTP/2 support</h2>
<p><a href="https://sethmlarson.dev/urllib3-is-fundraising-for-http2-support">urllib3 is raising ~$40,000 USD</a> to release HTTP/2 support and ensure long-term sustainable maintenance of the project after a sharp decline in financial support for 2023. If your company or organization uses Python and would benefit from HTTP/2 support in Requests, pip, cloud SDKs, and thousands of other projects <a href="https://opencollective.com/urllib3">please consider contributing financially</a> to ensure HTTP/2 support is developed sustainably and maintained for the long-haul.</p>
<p>Thank you for your support.</p>
<h2>Changes</h2>
<ul>
<li>Added the <code>Proxy-Authorization</code> header to the list of headers to strip from requests when redirecting to a different host. As before, different headers can be set via <code>Retry.remove_headers_on_redirect</code>.</li>
<li>Allowed passing negative integers as <code>amt</code> to read methods of <code>http.client.HTTPResponse</code> as an alternative to <code>None</code>. (<a href="">#3122</a>)</li>
<li>Fixed return types representing copying actions to use <code>typing.Self</code>. (<a href="">#3363</a>)</li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/urllib3/urllib3/compare/2.2.1...2.2.2">https://github.com/urllib3/urllib3/compare/2.2.1...2.2.2</a></p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/urllib3/urllib3/blob/main/CHANGES.rst">urllib3's changelog</a>.</em></p>
<blockquote>
<h1>2.2.2 (2024-06-17)</h1>
<ul>
<li>Added the <code>Proxy-Authorization</code> header to the list of headers to strip from requests when redirecting to a different host. As before, different headers can be set via <code>Retry.remove_headers_on_redirect</code>.</li>
<li>Allowed passing negative integers as <code>amt</code> to read methods of <code>http.client.HTTPResponse</code> as an alternative to <code>None</code>. (<code> &lt;</code>__)</li>
<li>Fixed return types representing copying actions to use <code>typing.Self</code>. (<code> &lt;</code>__)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>27e2a5c</code></a> Release 2.2.2 (<a href="">#3406</a>)</li>
<li><a href=""><code>accff72</code></a> Merge pull request from GHSA-34jh-p97f-mpxf</li>
<li><a href=""><code>34be4a5</code></a> Pin CFFI to a new release candidate instead of a Git commit (<a href="">#3398</a>)</li>
<li><a href=""><code>da41058</code></a> Bump browser-actions/setup-chrome from 1.6.0 to 1.7.1 (<a href="">#3399</a>)</li>
<li><a href=""><code>b07a669</code></a> Bump github/codeql-action from 2.13.4 to 3.25.6 (<a href="">#3396</a>)</li>
<li><a href=""><code>b8589ec</code></a> Measure coverage with v4 of artifact actions (<a href="">#3394</a>)</li>
<li><a href=""><code>f3bdc55</code></a> Allow triggering CI manually (<a href="">#3391</a>)</li>
<li><a href=""><code>5239265</code></a> Fix HTTP version in debug log (<a href="">#3316</a>)</li>
<li><a href=""><code>b34619f</code></a> Bump actions/checkout to 4.1.4 (<a href="">#3387</a>)</li>
<li><a href=""><code>9961d14</code></a> Bump browser-actions/setup-chrome from 1.5.0 to 1.6.0 (<a href="">#3386</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/urllib3/urllib3/compare/2.2.1...2.2.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=urllib3&package-manager=pip&previous-version=2.2.1&new-version=2.2.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ced8527a5481`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.