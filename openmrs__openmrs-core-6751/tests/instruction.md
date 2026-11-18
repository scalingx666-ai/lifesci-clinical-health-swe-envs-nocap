# Issue

**Title:** maven(deps): bump org.jobrunr:jobrunr from 9.0.1 to 9.0.2

## Description

Bumps [org.jobrunr:jobrunr](https://github.com/jobrunr/jobrunr) from 9.0.1 to 9.0.2.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/jobrunr/jobrunr/releases">org.jobrunr:jobrunr's releases</a>.</em></p>
<blockquote>
<h2>v9.0.2</h2>
<h1>Jobrunr and JobRunr Pro 9.0.2</h1>
<p>JobRunr 9.0.2 makes the JobRunrStarter Bean replaceable and makes use of suppliers to get all values for SQL query performance. JobRunr Pro 9.0.2 fixes an issue where the incorrect ClassLoader would be used on server recovery and fixes an issue for Oracle when the <code>jobAsJson</code> was too large.</p>
<h2>JobRunr 9.0.2</h2>
<h3>Enhancements</h3>
<ul>
<li>Make JobRunrStarter Bean replaceable. [PR <a href="">#1623</a>](<a href="">jobrunr/jobrunr#1623</a>)</li>
<li>Use suppliers to get values for SQL query parameters. [PR <a href="">#1624</a>](<a href="">jobrunr/jobrunr#1624</a>)</li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/jobrunr/jobrunr/compare/v9.0.1...v9.0.2">https://github.com/jobrunr/jobrunr/compare/v9.0.1...v9.0.2</a></p>
<h2>JobRunr Pro 9.0.2</h2>
<h3>Enhancements</h3>
<ul>
<li>Make JobRunrStarter Bean replaceable. [PR <a href="">#995</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/issues/995">https://git.jobrunr.io/JobRunr/jobrunr-pro/issues/995</a>) (from OSS [PR <a href="">#1623</a>](<a href="">jobrunr/jobrunr#1623</a>))</li>
<li>Use suppliers to get values for SQL query parameters. [PR <a href="">#995</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/issues/995">https://git.jobrunr.io/JobRunr/jobrunr-pro/issues/995</a>) (from OSS [PR <a href="">#1624</a>](<a href="">jobrunr/jobrunr#1624</a>))</li>
<li>Make <code>InMemoryTransport</code> the default event transport for <code>InMemoryStorageProvider</code>. [PR <a href="">#993</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/issues/993">https://git.jobrunr.io/JobRunr/jobrunr-pro/issues/993</a>)</li>
</ul>
<h3>Bugfixes</h3>
<ul>
<li>Keep application ClassLoader on server recovery. [PR <a href="">#997</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/issues/997">https://git.jobrunr.io/JobRunr/jobrunr-pro/issues/997</a>)</li>
<li>[Oracle] Fix <code>jobAsJson</code> value too large error on insertion. [PR <a href="">#1000</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/issues/1000">https://git.jobrunr.io/JobRunr/jobrunr-pro/issues/1000</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>783682b</code></a> Use suppliers to get values for SQL query parameters (<a href="">#1624</a>)</li>
<li><a href=""><code>79d4d23</code></a> Make JobRunrStarter Bean replaceable (<a href="">#1623</a>)</li>
<li>See full diff in <a href="https://github.com/jobrunr/jobrunr/compare/v9.0.1...v9.0.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.jobrunr:jobrunr&package-manager=maven&previous-version=9.0.1&new-version=9.0.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cc848fde7269`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.