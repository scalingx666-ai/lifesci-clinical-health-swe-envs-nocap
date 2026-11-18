# Issue

**Title:** maven(deps): bump org.jobrunr:jobrunr from 8.8.1 to 8.8.2

## Description

Bumps [org.jobrunr:jobrunr](https://github.com/jobrunr/jobrunr) from 8.8.1 to 8.8.2.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/jobrunr/jobrunr/releases">org.jobrunr:jobrunr's releases</a>.</em></p>
<blockquote>
<h2>v8.8.2</h2>
<h1>JobRunr and JobRunr Pro 8.8.2</h1>
<p>This release includes enhancements for JobRunr Pro to enable you to switch between slow and fast recurring runs and for JobRunr makes micronaut management optional. It also includes a security related bugfix for JobRunr Pro where the JobResult was not being redacted correctly.</p>
<h2>JobRunr 8.8.2</h2>
<h3>Enhancements</h3>
<ul>
<li>Make micronaut management optional [PR <a href="">#1599</a>](<a href="">jobrunr/jobrunr#1599</a>)</li>
</ul>
<h2>JobRunr Pro 8.8.2</h2>
<h3>Enhancements</h3>
<ul>
<li>Support switching between slow to fast recurring runs [PR <a href="">#934</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/934">https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/934</a>)</li>
<li>Make micronaut management optional [PR <a href="">#938</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/938">https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/938</a>) (from OSS [PR <a href="">#1599</a>](<a href="">jobrunr/jobrunr#1599</a>))</li>
</ul>
<h3>Bugfixes</h3>
<ul>
<li>Fix JobResult not being redacted correctly [PR <a href="">#937</a>](<a href="https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/937">https://git.jobrunr.io/JobRunr/jobrunr-pro/pulls/937</a>)</li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/jobrunr/jobrunr/compare/v8.8.1...v8.8.2">https://github.com/jobrunr/jobrunr/compare/v8.8.1...v8.8.2</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>77782cf</code></a> Make micronaut management optional (<a href="">#1599</a>)</li>
<li>See full diff in <a href="https://github.com/jobrunr/jobrunr/compare/v8.8.1...v8.8.2">compare view</a></li>
</ul>
</details>
<br />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `28e3bab9e206`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.