# Issue

**Title:** maven(deps): bump shedlockVersion from 7.8.0 to 7.9.0

## Description

Bumps `shedlockVersion` from 7.8.0 to 7.9.0.
Updates `net.javacrumbs.shedlock:shedlock-spring` from 7.8.0 to 7.9.0
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/lukas-krecan/ShedLock/blob/master/RELEASES.md">net.javacrumbs.shedlock:shedlock-spring's changelog</a>.</em></p>
<blockquote>
<h2>7.9.0 (2026-08-18)</h2>
<ul>
<li>Introduce NewTransactionRunner for jOOQ provider to solve <a href="">#3577</a> in case when a transaction is active</li>
<li>Improve transaction handling in Exposed when lock wrapped in a transaction</li>
<li>Dependency updates</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>dbb0ee9</code></a> [maven-release-plugin] prepare release shedlock-parent-7.9.0</li>
<li><a href=""><code>5a4cf23</code></a> README updated</li>
<li><a href=""><code>ee7df27</code></a> Introducing NewTransactionRunner (<a href="">#3670</a>)</li>
<li><a href=""><code>36712d1</code></a> Merge pull request <a href="">#3680</a> from lukas-krecan/dependabot/maven/org.apache.maven....</li>
<li><a href=""><code>498d5b2</code></a> Merge pull request <a href="">#3679</a> from lukas-krecan/dependabot/maven/micronaut-sourceg...</li>
<li><a href=""><code>378fd06</code></a> Merge pull request <a href="">#3681</a> from lukas-krecan/dependabot/maven/org.mongodb-mongo...</li>
<li><a href=""><code>e799350</code></a> Merge pull request <a href="">#3678</a> from lukas-krecan/dependabot/maven/org.mongodb-mongo...</li>
<li><a href=""><code>ac0ea4b</code></a> Merge pull request <a href="">#3677</a> from lukas-krecan/dependabot/maven/software.amazon.a...</li>
<li><a href=""><code>2b0e357</code></a> Bump org.mongodb:mongodb-driver-sync from 5.9.2 to 5.10.0</li>
<li><a href=""><code>49f98ba</code></a> Bump org.apache.maven.extensions:maven-build-cache-extension</li>
<li>Additional commits viewable in <a href="https://github.com/lukas-krecan/ShedLock/compare/shedlock-parent-7.8.0...shedlock-parent-7.9.0">compare view</a></li>
</ul>
</details>
<br />

Updates `net.javacrumbs.shedlock:shedlock-provider-jdbc-template` from 7.8.0 to 7.9.0

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e2056c9af903`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.