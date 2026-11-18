# Issue

**Title:** maven(deps): bump org.dbunit:dbunit from 3.3.0 to 3.4.0

## Description

Bumps [org.dbunit:dbunit](https://github.com/dbunit/dbunit-extension) from 3.3.0 to 3.4.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/dbunit/dbunit-extension/releases">org.dbunit:dbunit's releases</a>.</em></p>
<blockquote>
<h2>3.4.0</h2>
<h2>What's Changed</h2>
<ul>
<li>perf(database): Cache and reuse IDatabaseConnection across tests by <a href="https://github.com/jeffjensen"><code>@​jeffjensen</code></a> in <a href="">dbunit/dbunit-extension#801</a></li>
<li>fix(dataset): Stop TimestampDataType double-shifting TIMESTAMP WITH T… by <a href="https://github.com/jeffjensen"><code>@​jeffjensen</code></a> in <a href="">dbunit/dbunit-extension#834</a></li>
<li>Test/835 insertoperationit enabledifsystemproperty by <a href="https://github.com/jeffjensen"><code>@​jeffjensen</code></a> in <a href="">dbunit/dbunit-extension#836</a></li>
<li>ci(release): Add GitHub Discussion announcement to release workflow by <a href="https://github.com/jeffjensen"><code>@​jeffjensen</code></a> in <a href="">dbunit/dbunit-extension#838</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/dbunit/dbunit-extension/compare/dbunit-3.3.0...dbunit-3.4.0">https://github.com/dbunit/dbunit-extension/compare/dbunit-3.3.0...dbunit-3.4.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>b567a3c</code></a> [maven-release-plugin] prepare release dbunit-3.4.0</li>
<li><a href=""><code>bd6daee</code></a> chore(release): Prep 3.4.0</li>
<li><a href=""><code>0772b9c</code></a> ci(release): Add GitHub Discussion announcement to release workflow</li>
<li><a href=""><code>5caaa4b</code></a> docs(site): Add 3.3.0 to snapshot API link</li>
<li><a href=""><code>7153470</code></a> docs(site): Add per-release highlight notes to the News section</li>
<li><a href=""><code>8f8ed94</code></a> docs(changes): Summarize 3.4.0-SNAPSHOT release description instead of per-en...</li>
<li><a href=""><code>b15ed5b</code></a> docs(changes): Fix invalid and inaccurate type values in changes.xml entries</li>
<li><a href=""><code>11a9833</code></a> test(operation): Replace InsertOperationIT's inline HSQLDB-only assumeTrue wi...</li>
<li><a href=""><code>1e00a90</code></a> fix(dataset): Stop TimestampDataType double-shifting TIMESTAMP WITH TIME ZONE...</li>
<li><a href=""><code>892b2a1</code></a> fix(ant): Include csv in Export.setFormat's unsupported-format message</li>
<li>Additional commits viewable in <a href="https://github.com/dbunit/dbunit-extension/compare/dbunit-3.3.0...dbunit-3.4.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.dbunit:dbunit&package-manager=maven&previous-version=3.3.0&new-version=3.4.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e20185094abb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.