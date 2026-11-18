# Issue

**Title:** maven(deps): bump shedlockVersion from 7.10.0 to 7.10.1

## Description

Bumps `shedlockVersion` from 7.10.0 to 7.10.1.
Updates `net.javacrumbs.shedlock:shedlock-spring` from 7.10.0 to 7.10.1
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/lukas-krecan/ShedLock/blob/master/RELEASES.md">net.javacrumbs.shedlock:shedlock-spring's changelog</a>.</em></p>
<blockquote>
<h2>7.10.1 (2026-09-08)</h2>
<ul>
<li>Fix Neo4j ordering for lock extension <a href="">#3739</a></li>
<li>Dependency updates</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>c88efaf</code></a> [maven-release-plugin] prepare release shedlock-parent-7.10.1</li>
<li><a href=""><code>c04fa6e</code></a> Merge pull request <a href="">#3726</a> from lukas-krecan/dependabot/maven/org.apache.maven....</li>
<li><a href=""><code>58f553f</code></a> Fix Neo4j timestamp ordering for lock extension</li>
<li><a href=""><code>ae19412</code></a> Drop logback dep</li>
<li><a href=""><code>0babdd4</code></a> Bump org.apache.maven.plugins:maven-surefire-plugin from 3.5.6 to 3.6.0</li>
<li><a href=""><code>25711ae</code></a> Bump com.github.spotbugs:spotbugs-maven-plugin from 4.10.4.0 to 4.10.4.1</li>
<li><a href=""><code>e745628</code></a> Merge pull request <a href="">#3737</a> from lukas-krecan/dependabot/maven/com.diffplug.spot...</li>
<li><a href=""><code>4cebf50</code></a> Merge pull request <a href="">#3738</a> from lukas-krecan/dependabot/maven/com.h2database-h2...</li>
<li><a href=""><code>c074db4</code></a> Merge pull request <a href="">#3735</a> from lukas-krecan/dependabot/maven/com.google.cloud-...</li>
<li><a href=""><code>8b6af81</code></a> Bump com.h2database:h2 from 2.4.240 to 2.5.250</li>
<li>Additional commits viewable in <a href="https://github.com/lukas-krecan/ShedLock/compare/shedlock-parent-7.10.0...shedlock-parent-7.10.1">compare view</a></li>
</ul>
</details>
<br />

Updates `net.javacrumbs.shedlock:shedlock-provider-jdbc-template` from 7.10.0 to 7.10.1

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f06c26ac7b79`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.