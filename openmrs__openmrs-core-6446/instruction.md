# Issue

**Title:** maven(deps): bump org.jobrunr:jobrunr from 8.8.0 to 8.8.1

## Description

Bumps [org.jobrunr:jobrunr](https://github.com/jobrunr/jobrunr) from 8.8.0 to 8.8.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/jobrunr/jobrunr/releases">org.jobrunr:jobrunr's releases</a>.</em></p>
<blockquote>
<h2>v8.8.1</h2>
<h1>JobRunr and JobRunr Pro 8.8.1</h1>
<p>This release moves job retention from the background job server to a global configuration, making it available to all JobRunr components. It also adds Amazon DocumentDB autoconfiguration for Micronaut, and JobRunr Pro fixes automatic deletion of ExternalJobs.</p>
<blockquote>
<p>Heads-up: This release deprecates the existing job retention settings under background-job-server. Job retention is now configured at the jobs level. Please migrate to the new configuration as soon as possible. See [PR <a href="">#1592</a>](<a href="">jobrunr/jobrunr#1592</a>) for migration details.</p>
</blockquote>
<h2>JobRunr 8.8.1</h2>
<h3>Enhancements</h3>
<ul>
<li>[Micronaut] Autoconfigure Amazon DocumentDB. [PR <a href="">#1591</a>](<a href="">jobrunr/jobrunr#1591</a>)</li>
<li>Make job retention configuration a global configuration. [PR <a href="">#1592</a>](<a href="">jobrunr/jobrunr#1592</a>)</li>
</ul>
<h2>JobRunr Pro 8.8.1</h2>
<h3>Enhancements</h3>
<ul>
<li>[Micronaut] Autoconfigure Amazon DocumentDB. [PR <a href="">#931</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/931">https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/931</a>) (from OSS [PR <a href="">#1591</a>](<a href="">jobrunr/jobrunr#1591</a>))</li>
<li>Make job retention configuration a global configuration. [PR <a href="">#929</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/929">https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/929</a>), [PR <a href="">#931</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/931">https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/931</a>) (from OSS [PR <a href="">#1592</a>](<a href="">jobrunr/jobrunr#1592</a>))</li>
</ul>
<h3>Bugfixes</h3>
<ul>
<li>Fix automatic deletion of <code>ExternalJob</code>s. [PR <a href="">#929</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/929">https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/929</a>)</li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/jobrunr/jobrunr/compare/v8.8.0...v8.8.1">https://github.com/jobrunr/jobrunr/compare/v8.8.0...v8.8.1</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>c7066ed</code></a> Make job retention configuration a global configuration (<a href="">#1592</a>)</li>
<li><a href=""><code>c84222a</code></a> [Micronaut] Autoconfigure Amazon DocumentDB (<a href="">#1591</a>)</li>
<li>See full diff in <a href="https://github.com/jobrunr/jobrunr/compare/v8.8.0...v8.8.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.jobrunr:jobrunr&package-manager=maven&previous-version=8.8.0&new-version=8.8.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1c71dca2e9cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.