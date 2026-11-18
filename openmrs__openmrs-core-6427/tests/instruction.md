# Issue

**Title:** maven(deps): bump org.jobrunr:jobrunr from 8.7.1 to 8.8.0

## Description

Bumps [org.jobrunr:jobrunr](https://github.com/jobrunr/jobrunr) from 8.7.1 to 8.8.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/jobrunr/jobrunr/releases">org.jobrunr:jobrunr's releases</a>.</em></p>
<blockquote>
<h2>v8.8.0</h2>
<h1>JobRunr and JobRunr Pro 8.8.0</h1>
<p>JobRunr 8.8.0 comes with reduced logging in case of StorageProvider exceptions, along with several enhancements and bugfixes. Quarkus users would be happy to learn that SmallRye is no longer a required dependency. JobRunr Pro 8.8.0 also introduces performance improvements for MySQL with large amounts of jobs.</p>
<h3>Highlighted changes</h3>
<ul>
<li><strong>Reduced BackgroundJobServer logging</strong></li>
</ul>
<p>We've improved the log message when a BackgroundJobServer encounters a StorageException. And more importantly, the log level is raised incrementally.</p>
<ul>
<li><strong>Removed SmallRye requirement</strong></li>
</ul>
<p>Quarkus users may now remove the <code>quarkus-smallrye-health</code> dependency, as it's no longer required to run JobRunr with the Quarkus Extension. Keep it if you want JobRunr to contribute to the health endpoint, drop it otherwise.</p>
<ul>
<li><strong>Kotlin 2.4 support</strong></li>
</ul>
<p>We've tested against Kotlin 2.4 and can confirm its official support.</p>
<ul>
<li><strong>Dashboard and SQL Database performance improvements (Pro)</strong></li>
</ul>
<p>We've done improvements to database queries which will result in the Dashboard loading faster.</p>
<p>⚠️ Note that this comes with new database migrations, involving dropping and creating indexes.</p>
<h2>JobRunr 8.8.0</h2>
<h3>Enhancements</h3>
<ul>
<li>[Quarkus] Remove Smallrye requirement [PR <a href="">#1589</a>](<a href="">jobrunr/jobrunr#1589</a>)</li>
<li>Reduce logging in case of StorageProvider exceptions [PR <a href="">#1587</a>](<a href="">jobrunr/jobrunr#1587</a>)</li>
</ul>
<h3>Bugfixes</h3>
<ul>
<li>Prevent time-to-check to time-to-use race condition in DatabaseCreator [PR <a href="">#1583</a>](<a href="">jobrunr/jobrunr#1583</a>)</li>
</ul>
<h3>Misc</h3>
<ul>
<li>Update dependencies [PR <a href="">#1588</a>](<a href="">jobrunr/jobrunr#1588</a>)</li>
</ul>
<h2>JobRunr Pro 8.8.0</h2>
<h3>Enhancements</h3>
<ul>
<li>[Quarkus] Remove Smallrye requirement [PR <a href="">#927</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/927">https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/927</a>) (from OSS [PR <a href="">#1589</a>](<a href="">jobrunr/jobrunr#1589</a>))</li>
<li>Improve dashboard performance for MySQL and other databases [PR <a href="">#922</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/922">https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/922</a>)</li>
<li>Reduce logging in case of StorageProvider exceptions [PR <a href="">#927</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/927">https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/927</a>) (from OSS [PR <a href="">#1587</a>](<a href="">jobrunr/jobrunr#1587</a>))</li>
</ul>
<h3>Bugfixes</h3>
<ul>
<li>Fix filters not applying correctly in queries once locked [PR <a href="">#920</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/920">https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/920</a>), [PR <a href="">#922</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/922">https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/922</a>)</li>
<li>Throw when rate-limited job is provided a different limiter [PR <a href="">#924</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/924">https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/924</a>)</li>
<li>Fix batch child status being disregarded in JobRequestScheduler#enqueue(Stream<!-- raw HTML omitted -->) [PR <a href="">#923</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/923">https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/923</a>)</li>
<li>Prevent time-to-check to time-to-use race condition in DatabaseCreator [PR <a href="">#919</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/919">https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/919</a>) (from OSS [PR <a href="">#1583</a>](<a href="">jobrunr/jobrunr#1583</a>))</li>
</ul>
<h3>Misc</h3>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>adbee0b</code></a> Update dependencies (<a href="">#1588</a>)</li>
<li><a href=""><code>e2e3f45</code></a> Remove Smallrye requirement (<a href="">#1589</a>)</li>
<li><a href=""><code>587e4a7</code></a> Reduce logging in case of StorageProvider exceptions (<a href="">#1587</a>)</li>
<li><a href=""><code>5fea38e</code></a> Prevent time-to-check to time-to-use race condition in DatabaseCreator (<a href="">#1583</a>)</li>
<li>See full diff in <a href="https://github.com/jobrunr/jobrunr/compare/v8.7.1...v8.8.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.jobrunr:jobrunr&package-manager=maven&previous-version=8.7.1&new-version=8.8.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e3331f69a987`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.