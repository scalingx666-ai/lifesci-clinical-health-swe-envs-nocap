# Issue

**Title:** maven(deps): bump com.github.spotbugs:spotbugs-maven-plugin from 4.10.3.0 to 4.10.4.0

## Description

Bumps [com.github.spotbugs:spotbugs-maven-plugin](https://github.com/spotbugs/spotbugs-maven-plugin) from 4.10.3.0 to 4.10.4.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/spotbugs/spotbugs-maven-plugin/releases">com.github.spotbugs:spotbugs-maven-plugin's releases</a>.</em></p>
<blockquote>
<h2>spotbugs-maven-plugin-4.10.4.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Fixes <a href="">#1474</a> by <a href="https://github.com/gigabitzauber"><code>@​gigabitzauber</code></a> in <a href="">spotbugs/spotbugs-maven-plugin#1487</a></li>
<li>Update build by <a href="https://github.com/hazendaz"><code>@​hazendaz</code></a> in <a href="">spotbugs/spotbugs-maven-plugin#1494</a></li>
<li>Cleanup charset handling and remove never used sourceEncoding in spot… by <a href="https://github.com/hazendaz"><code>@​hazendaz</code></a> in <a href="">spotbugs/spotbugs-maven-plugin#1495</a></li>
<li>Improve javaExecutable usage to prefer current process by <a href="https://github.com/hazendaz"><code>@​hazendaz</code></a> in <a href="">spotbugs/spotbugs-maven-plugin#1496</a></li>
<li>Update deprecated artifact handling by <a href="https://github.com/hazendaz"><code>@​hazendaz</code></a> in <a href="">spotbugs/spotbugs-maven-plugin#1497</a></li>
<li>Require maven 3.8.9 or better by <a href="https://github.com/hazendaz"><code>@​hazendaz</code></a> in <a href="">spotbugs/spotbugs-maven-plugin#1499</a></li>
<li>Add missing javadocs by <a href="https://github.com/hazendaz"><code>@​hazendaz</code></a> in <a href="">spotbugs/spotbugs-maven-plugin#1500</a></li>
<li>Otherwise build updates and library updates</li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/gigabitzauber"><code>@​gigabitzauber</code></a> made their first contribution in <a href="">spotbugs/spotbugs-maven-plugin#1487</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/spotbugs/spotbugs-maven-plugin/compare/spotbugs-maven-plugin-4.10.3.0...spotbugs-maven-plugin-4.10.4.0">https://github.com/spotbugs/spotbugs-maven-plugin/compare/spotbugs-maven-plugin-4.10.3.0...spotbugs-maven-plugin-4.10.4.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>698cfa7</code></a> [maven-release-plugin] prepare release spotbugs-maven-plugin-4.10.4.0</li>
<li><a href=""><code>f12b09f</code></a> [pom] Update spotbugs core to 4.10.4</li>
<li><a href=""><code>2fc78c6</code></a> Merge pull request <a href="">#1500</a> from hazendaz/master</li>
<li><a href=""><code>87e41d6</code></a> Add more missing javadocs throughout</li>
<li><a href=""><code>b2149c3</code></a> [docs] Add missing javadocs to rest of integration tests</li>
<li><a href=""><code>6cdda40</code></a> Merge pull request <a href="">#1499</a> from hazendaz/master</li>
<li><a href=""><code>d9d54a6</code></a> Merge pull request <a href="">#1498</a> from spotbugs/renovate/byte-buddy.version</li>
<li><a href=""><code>54738d7</code></a> Require maven 3.8.9 or better</li>
<li><a href=""><code>d3646ee</code></a> Update byte-buddy.version to v1.18.12</li>
<li><a href=""><code>011cbec</code></a> Merge pull request <a href="">#1497</a> from hazendaz/master</li>
<li>Additional commits viewable in <a href="https://github.com/spotbugs/spotbugs-maven-plugin/compare/spotbugs-maven-plugin-4.10.3.0...spotbugs-maven-plugin-4.10.4.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=com.github.spotbugs:spotbugs-maven-plugin&package-manager=maven&previous-version=4.10.3.0&new-version=4.10.4.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2ce847744295`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.