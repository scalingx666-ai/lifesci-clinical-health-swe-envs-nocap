# Issue

**Title:** github-actions(deps): bump actions/setup-java from 6.1.0 to 6.2.0

## Description

Bumps [actions/setup-java](https://github.com/actions/setup-java) from 6.1.0 to 6.2.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/setup-java/releases">actions/setup-java's releases</a>.</em></p>
<blockquote>
<h2>v6.2.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Fix Liberica SDKMAN patch release resolution by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1291</a></li>
<li>Update Undici to 6.29.1 by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1308</a></li>
<li>chore(deps): bump the monthly-npm-updates group with 12 updates by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/setup-java#1309</a></li>
<li>Fix Liberica Java 25 release resolution by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1313</a></li>
<li>Add repository-specific Copilot instructions by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1312</a></li>
<li>Support exact Corretto release versions by <a href="https://github.com/electrum"><code>@​electrum</code></a> in <a href="">actions/setup-java#1310</a></li>
<li>Support Maven mirrors in generated settings.xml by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1289</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/electrum"><code>@​electrum</code></a> made their first contribution in <a href="">actions/setup-java#1310</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/setup-java/compare/v6.1.0...v6.2.0">https://github.com/actions/setup-java/compare/v6.1.0...v6.2.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>77dd5b2</code></a> Support Maven mirrors in generated settings.xml (<a href="">#1289</a>)</li>
<li><a href=""><code>644a850</code></a> Support exact Corretto release versions (<a href="">#1310</a>)</li>
<li><a href=""><code>dade0c5</code></a> Save uncommitted changes (<a href="">#1312</a>)</li>
<li><a href=""><code>ef0b922</code></a> Fix Liberica Java 25 release resolution (<a href="">#1313</a>)</li>
<li><a href=""><code>e144521</code></a> chore(deps): bump the monthly-npm-updates group with 12 updates (<a href="">#1309</a>)</li>
<li><a href=""><code>8cd57eb</code></a> Update Undici to 6.29.1 (<a href="">#1308</a>)</li>
<li><a href=""><code>816722a</code></a> Fix Liberica SDKMAN patch release resolution (<a href="">#1291</a>)</li>
<li>See full diff in <a href="https://github.com/actions/setup-java/compare/v6.1.0...v6.2.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/setup-java&package-manager=github_actions&previous-version=6.1.0&new-version=6.2.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7adee79ba78f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.