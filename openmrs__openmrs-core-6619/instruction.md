# Issue

**Title:** maven(deps): bump com.h2database:h2 from 2.5.250 to 2.5.252

## Description

Bumps [com.h2database:h2](https://github.com/h2database/h2database) from 2.5.250 to 2.5.252.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/h2database/h2database/releases">com.h2database:h2's releases</a>.</em></p>
<blockquote>
<h2>Version 2.5.252</h2>
<!-- raw HTML omitted -->
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>f986838</code></a> in preparation for a release</li>
<li><a href=""><code>06c34a7</code></a> Merge pull request <a href="">#4418</a> from andreitokar/issues-4380-4376</li>
<li><a href=""><code>1aef3e0</code></a> <a href="">#4376</a>: Reading INFORMATION_SCHEMA.COLUMNS fails with a NPE while any material...</li>
<li><a href=""><code>4bb8aee</code></a> <a href="">#4380</a>: creating a MATERIALIZED VIEW makes a persistent database permanently u...</li>
<li><a href=""><code>95b6af0</code></a> Merge pull request <a href="">#4417</a> from andreitokar/issue-4395</li>
<li><a href=""><code>6ec30b6</code></a> <a href="">#4395</a> disallow constraints between temporary and permanent tables</li>
<li><a href=""><code>0f0f856</code></a> Merge pull request <a href="">#4416</a> from andreitokar/issue-4405</li>
<li><a href=""><code>f718b76</code></a> <a href="">#4405</a> SecureFileStore.readFully() may skip decryption</li>
<li><a href=""><code>e231ff7</code></a> <a href="">#4405</a> SecureFileStore.readFully() may skip</li>
<li><a href=""><code>4da0d1d</code></a> Merge pull request <a href="">#4415</a> from jjh75607/fix/log-sql-aarch64</li>
<li>Additional commits viewable in <a href="https://github.com/h2database/h2database/compare/version-2.5.250...version-2.5.252">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=com.h2database:h2&package-manager=maven&previous-version=2.5.250&new-version=2.5.252)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1222cf828bae`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.