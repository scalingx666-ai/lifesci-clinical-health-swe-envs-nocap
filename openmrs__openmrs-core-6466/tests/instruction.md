# Issue

**Title:** maven(deps): bump shedlockVersion from 7.7.0 to 7.8.0

## Description

Bumps `shedlockVersion` from 7.7.0 to 7.8.0.
Updates `net.javacrumbs.shedlock:shedlock-spring` from 7.7.0 to 7.8.0
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/lukas-krecan/ShedLock/blob/master/RELEASES.md">net.javacrumbs.shedlock:shedlock-spring's changelog</a>.</em></p>
<blockquote>
<h2>7.8.0 (2026-08-13)</h2>
<ul>
<li>Fix S3LockProvider 409 Conflict handling <a href="">#3662</a></li>
<li>Dependency updates</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>842143e</code></a> [maven-release-plugin] prepare release shedlock-parent-7.8.0</li>
<li><a href=""><code>6b61937</code></a> Skip test on release</li>
<li><a href=""><code>f882e3f</code></a> Drop oss-parent</li>
<li><a href=""><code>3a96a53</code></a> Bump redis.clients:jedis from 7.5.3 to 8.0.0 (<a href="">#3666</a>)</li>
<li><a href=""><code>af5e29e</code></a> Fix release</li>
<li><a href=""><code>02b5085</code></a> [maven-release-plugin] rollback the release of shedlock-parent-7.8.0</li>
<li><a href=""><code>64dbf3d</code></a> [maven-release-plugin] prepare for next development iteration</li>
<li><a href=""><code>5216b62</code></a> Fix release</li>
<li><a href=""><code>2d6e83f</code></a> Pin Kotlin target (<a href="">#3664</a>)</li>
<li><a href=""><code>c99c885</code></a> <a href="">#3662</a> Fix Handling of 409 in S3LockProvider (<a href="">#3663</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/lukas-krecan/ShedLock/compare/shedlock-parent-7.7.0...shedlock-parent-7.8.0">compare view</a></li>
</ul>
</details>
<br />

Updates `net.javacrumbs.shedlock:shedlock-provider-jdbc-template` from 7.7.0 to 7.8.0

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `960f1cb95496`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.