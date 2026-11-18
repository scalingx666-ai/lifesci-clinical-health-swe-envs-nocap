# Issue

**Title:** maven(deps): bump shedlockVersion from 7.9.0 to 7.10.0

## Description

Bumps `shedlockVersion` from 7.9.0 to 7.10.0.
Updates `net.javacrumbs.shedlock:shedlock-spring` from 7.9.0 to 7.10.0
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/lukas-krecan/ShedLock/blob/master/RELEASES.md">net.javacrumbs.shedlock:shedlock-spring's changelog</a>.</em></p>
<blockquote>
<h2>7.10.0 (2026-09-04)</h2>
<ul>
<li>Add datasource-backed transaction runner for jOOQ provider <a href="">#3683</a></li>
<li>Dependency updates</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>0fb7458</code></a> [maven-release-plugin] prepare release shedlock-parent-7.10.0</li>
<li><a href=""><code>af429a7</code></a> Use maven wrapper 3 (<a href="">#3730</a>)</li>
<li><a href=""><code>dd533c4</code></a> <a href="">#3683</a> Introduce JooqTransactionRunner (<a href="">#3725</a>)</li>
<li><a href=""><code>d628e8d</code></a> Upgrade jOOQ</li>
<li><a href=""><code>7099a96</code></a> Merge pull request <a href="">#3729</a> from lukas-krecan/dependabot/maven/software.amazon.a...</li>
<li><a href=""><code>b20fbf0</code></a> Merge pull request <a href="">#3727</a> from lukas-krecan/dependabot/maven/vertx.version-5.1.7</li>
<li><a href=""><code>445df33</code></a> Merge pull request <a href="">#3728</a> from lukas-krecan/dependabot/maven/co.elastic.client...</li>
<li><a href=""><code>cbbcb82</code></a> Bump software.amazon.awssdk:s3 from 2.54.7 to 2.54.9</li>
<li><a href=""><code>d4b1fe9</code></a> Bump co.elastic.clients:elasticsearch-java from 9.5.2 to 9.5.3</li>
<li><a href=""><code>d352e31</code></a> Bump vertx.version from 5.1.6 to 5.1.7</li>
<li>Additional commits viewable in <a href="https://github.com/lukas-krecan/ShedLock/compare/shedlock-parent-7.9.0...shedlock-parent-7.10.0">compare view</a></li>
</ul>
</details>
<br />

Updates `net.javacrumbs.shedlock:shedlock-provider-jdbc-template` from 7.9.0 to 7.10.0

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `24946d82274e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.