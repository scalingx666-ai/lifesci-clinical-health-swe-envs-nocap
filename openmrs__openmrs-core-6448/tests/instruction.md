# Issue

**Title:** maven(deps): bump org.junit:junit-bom from 6.1.2 to 6.1.3

## Description

Bumps [org.junit:junit-bom](https://github.com/junit-team/junit-framework) from 6.1.2 to 6.1.3.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/junit-team/junit-framework/releases">org.junit:junit-bom's releases</a>.</em></p>
<blockquote>
<p>JUnit 6.1.3 = Platform 6.1.3 + Jupiter 6.1.3 + Vintage 6.1.3</p>
<p>See <a href="https://docs.junit.org/6.1.3/release-notes.html">Release Notes</a>.</p>
<p><strong>Full Changelog</strong>: <a href="https://github.com/junit-team/junit-framework/compare/r6.1.2...r6.1.3">https://github.com/junit-team/junit-framework/compare/r6.1.2...r6.1.3</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>f59f60d</code></a> Release 6.1.3</li>
<li><a href=""><code>cd8ec92</code></a> Finalize 6.1.3 release notes</li>
<li><a href=""><code>c8729f2</code></a> Restore compatibility with GraalVM 25 (<a href="">#5901</a>)</li>
<li><a href=""><code>ddc9e74</code></a> Update graalvm/setup-graalvm action to v1.6.4 (<a href="">#5959</a>)</li>
<li><a href=""><code>fe2c52a</code></a> Update plugin org.graalvm.buildtools.native to v1.1.7 (<a href="">#5923</a>)</li>
<li><a href=""><code>62afc02</code></a> Delay GraalVM plugin updates for 3 days</li>
<li><a href=""><code>0cc2902</code></a> Skip <code>graalVmTest</code> task if GraalVM env vars are not set</li>
<li><a href=""><code>f6bbfc5</code></a> Move GraalVM tests to separate test task (<a href="">#5903</a>)</li>
<li><a href=""><code>e87e052</code></a> Update plugin org.graalvm.buildtools.native to v1.1.6 (<a href="">#5899</a>)</li>
<li><a href=""><code>1cd56df</code></a> Update plugin org.graalvm.buildtools.native to v1.1.5 (<a href="">#5880</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/junit-team/junit-framework/compare/r6.1.2...r6.1.3">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.junit:junit-bom&package-manager=maven&previous-version=6.1.2&new-version=6.1.3)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1c71dca2e9cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.