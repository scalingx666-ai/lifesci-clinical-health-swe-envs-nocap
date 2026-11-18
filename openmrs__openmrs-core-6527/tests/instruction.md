# Issue

**Title:** maven(deps): bump com.diffplug.spotless:spotless-maven-plugin from 3.10.0 to 3.10.1

## Description

Bumps [com.diffplug.spotless:spotless-maven-plugin](https://github.com/diffplug/spotless) from 3.10.0 to 3.10.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/diffplug/spotless/releases">com.diffplug.spotless:spotless-maven-plugin's releases</a>.</em></p>
<blockquote>
<h2>Maven Plugin v3.10.1</h2>
<h3>Fixed</h3>
<ul>
<li><code>&lt;prettier&gt;</code> and other npm-based steps no longer fail to start on npm 12 (<code>EUNKNOWNCONFIG</code> from <code>--scripts-prepend-node-path</code>). (<a href="">#3024</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>4ea1c6c</code></a> Published maven/3.10.1</li>
<li><a href=""><code>f2f2348</code></a> Published gradle/8.10.1</li>
<li><a href=""><code>4bc8980</code></a> Published lib/4.10.1</li>
<li><a href=""><code>6fedfd5</code></a> chore(deps): update plugin errorprone to v5.1.1 (<a href="">#3035</a>)</li>
<li><a href=""><code>5e10f0b</code></a> chore(deps): update plugin errorprone to v5.1.1</li>
<li><a href=""><code>3aa82b5</code></a> fix: expand a directory passed to targetExclude into the files under it (<a href="">#3032</a>)</li>
<li><a href=""><code>68bddde</code></a> shortenFullyQualifiedTypes: skip FQNs whose simple name clashes with types de...</li>
<li><a href=""><code>6f73ed3</code></a> fix(deps): update dependency org.codehaus.plexus:plexus-utils to v4.1.0 (<a href="">#3030</a>)</li>
<li><a href=""><code>bdeafe7</code></a> docs: changelog entry for the targetExclude directory fix</li>
<li><a href=""><code>4187eb3</code></a> fix: expand a directory passed to targetExclude into the files under it</li>
<li>Additional commits viewable in <a href="https://github.com/diffplug/spotless/compare/maven/3.10.0...maven/3.10.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=com.diffplug.spotless:spotless-maven-plugin&package-manager=maven&previous-version=3.10.0&new-version=3.10.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `be8716784e90`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.