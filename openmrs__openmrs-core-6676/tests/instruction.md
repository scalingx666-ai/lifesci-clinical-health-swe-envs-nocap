# Issue

**Title:** maven(deps): bump org.jobrunr:jobrunr from 9.0.0 to 9.0.1

## Description

Bumps [org.jobrunr:jobrunr](https://github.com/jobrunr/jobrunr) from 9.0.0 to 9.0.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/jobrunr/jobrunr/releases">org.jobrunr:jobrunr's releases</a>.</em></p>
<blockquote>
<h2>v9.0.1</h2>
<h1>JobRunr and JobRunr Pro 9.0.1</h1>
<p>JobRunr 9.0.1 brings a fix to the automatic module name for our spring boot starters. JobRunr Pro 9.0.1 also brings a default constructor to policy type enums, a critical fix to the ProcessBatchJobsTask and a few other minor changes.</p>
<h2>JobRunr 9.0.1</h2>
<h3>Bugfix</h3>
<ul>
<li>Fix automatic module name for Spring Boot Starters. [PR <a href="">#1620</a>](<a href="">jobrunr/jobrunr#1620</a>)</li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/jobrunr/jobrunr/compare/v9.0.0...v9.0.1">https://github.com/jobrunr/jobrunr/compare/v9.0.0...v9.0.1</a></p>
<h2>JobRunr Pro 9.0.1</h2>
<h3>Enhancements</h3>
<ul>
<li>Add a default constructor to policy type enums. [PR <a href="">#987</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/987">https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/987</a>)</li>
</ul>
<h3>Bugfixes</h3>
<ul>
<li>Handle all standard OpenID authentication error codes. [PR <a href="">#989</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/989">https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/989</a>)</li>
<li>Prevent ProcessBatchJobsTask from succeeding non-paused awaiting BatchJobs. [PR <a href="">#991</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/991">https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/991</a>)</li>
<li>Show requeue message when using shceduleAt with requeue. [PR <a href="">#992</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/992">https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/992</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>79a44ac</code></a> Fix automatic module name for Spring Boot Starters (<a href="">#1620</a>)</li>
<li>See full diff in <a href="https://github.com/jobrunr/jobrunr/compare/v9.0.0...v9.0.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.jobrunr:jobrunr&package-manager=maven&previous-version=9.0.0&new-version=9.0.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a69b14a84bf9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.