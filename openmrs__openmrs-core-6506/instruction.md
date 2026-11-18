# Issue

**Title:** maven(deps): bump org.javassist:javassist from 3.32.0-GA to 3.33.0-GA

## Description

Bumps [org.javassist:javassist](https://github.com/jboss-javassist/javassist) from 3.32.0-GA to 3.33.0-GA.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/jboss-javassist/javassist/releases">org.javassist:javassist's releases</a>.</em></p>
<blockquote>
<h2>Javassist-3.33.0-GA</h2>
<h2>What's Changed</h2>
<ul>
<li>Fix SerialVersionUID for static nested classes by <a href="https://github.com/arimu1"><code>@​arimu1</code></a> in <a href="">jboss-javassist/javassist#523</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/jboss-javassist/javassist/compare/rel_3_32_0_ga...rel_3_33_0_ga">https://github.com/jboss-javassist/javassist/compare/rel_3_32_0_ga...rel_3_33_0_ga</a></p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/jboss-javassist/javassist/blob/master/Changes.md">org.javassist:javassist's changelog</a>.</em></p>
<blockquote>
<h3>Changes</h3>
<h3>version 3.33 on August 23, 2026</h3>
<ul>
<li>
<p>API changes suggested by <code>@waydeshi</code> and <code>@lucianjohnhouse</code></p>
</li>
<li>
<p>GitHub PR <a href="">#523</a></p>
</li>
</ul>
<h3>version 3.32 on June 21, 2026</h3>
<ul>
<li>
<p>API change suggested by Wayde Shi (GitHub: <code>@waydeshi</code>).</p>
</li>
<li>
<p>Excludes javassist.tools.{reflect,rmi,web}.  They are now included in ./examples/src/main.</p>
</li>
<li>
<p>Disables javassist.runtime.Desc.useContextClassLoader</p>
</li>
</ul>
<h3>version 3.31.0 on April 20, 2026</h3>
<ul>
<li>GitHub PR <a href="">#480</a>, <a href="">#484</a>, <a href="">#486</a>, <a href="">#491</a>, <a href="">#492</a>, <a href="">#495</a>, <a href="">#506</a></li>
</ul>
<h3>version 3.30.2 on December 25, 2023</h3>
<ul>
<li>GitHub PR <a href="">#473</a>, 475, 476</li>
</ul>
<h4>version 3.30.1 on December 17, 2023</h4>
<ul>
<li>GitHub Issue <a href="">#471</a></li>
</ul>
<h4>version 3.30 on December 17, 2023</h4>
<ul>
<li>GitHub PR <a href="">#434</a>, 448, 463 (Issue <a href="">#462</a>), 466, 467, 468, 469, 470,</li>
</ul>
<h4>version 3.29.2 on September 14, 2022</h4>
<ul>
<li>GitHub Issue <a href="">#427</a>.</li>
</ul>
<h4>version 3.29.1 on August 11, 2022</h4>
<ul>
<li>
<p>GitHub Issue <a href="">#423</a>.</p>
</li>
<li>
<p><code>Readme.html</code> was deleted (GitHub Issue <a href="">#414</a>).</p>
</li>
</ul>
<h4>version 3.29 on May 13, 2022</h4>
<ul>
<li>GitHub Issue <a href="">#378</a>, PR <a href="">#278</a>, <a href="">#299</a>, <a href="">#382</a>, <a href="">#383</a>, <a href="">#390</a>, <a href="">#391</a>, <a href="">#395</a>, <a href="">#399</a>, <a href="">#409</a>.</li>
</ul>
<h4>version 3.28 on May 8, 2021</h4>
<ul>
<li>GitHub Issue <a href="">#305</a>, <a href="">#328</a>, <a href="">#339</a>, <a href="">#350</a>, <a href="">#357</a>, and PR <a href="">#363</a>.</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li>See full diff in <a href="https://github.com/jboss-javassist/javassist/commits">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.javassist:javassist&package-manager=maven&previous-version=3.32.0-GA&new-version=3.33.0-GA)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3310bc1d9682`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.