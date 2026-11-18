# Issue

**Title:** maven(deps): bump com.diffplug.spotless:spotless-maven-plugin from 3.10.1 to 3.10.2

## Description

Bumps [com.diffplug.spotless:spotless-maven-plugin](https://github.com/diffplug/spotless) from 3.10.1 to 3.10.2.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/diffplug/spotless/releases">com.diffplug.spotless:spotless-maven-plugin's releases</a>.</em></p>
<blockquote>
<h2>Maven Plugin v3.10.2</h2>
<h3>Fixed</h3>
<ul>
<li><code>&lt;shortenFullyQualifiedTypes&gt;</code> now shortens fully-qualified types used in expression contexts (such as static method calls, static fields, and enum constants) while avoiding imports that would change how existing unqualified type references resolve. (<a href="">#3039</a>)</li>
<li>Eclipse JDT formatter step no longer fails with <code>NoClassDefFoundError</code> when lombok is active as a JVM agent (e.g. <code>-javaagent:lombok.jar</code> in Eclipse/VS Code/Cursor). (<a href="">#2795</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>dc2a4cb</code></a> Published maven/3.10.2</li>
<li><a href=""><code>876c8c4</code></a> Published gradle/8.10.2</li>
<li><a href=""><code>ff28375</code></a> Published lib/4.10.2</li>
<li><a href=""><code>e260aa7</code></a> shortenFullyQualifiedTypes: preserve unqualified type resolution (<a href="">#3037</a>)</li>
<li><a href=""><code>5a2cdca</code></a> Update changelogs.</li>
<li><a href=""><code>98ca50e</code></a> Merge remote-tracking branch 'origin/main' into 3033-unqualified-type-collision</li>
<li><a href=""><code>9591d7e</code></a> Resolve interopability with spotless, lombok and VSCode (<a href="">#3038</a>)</li>
<li><a href=""><code>5842e1b</code></a> shortenFullyQualifiedTypes: shorten FQTs in expression context (<a href="">#3039</a>)</li>
<li><a href=""><code>e7f5b60</code></a> Add changelog entries</li>
<li><a href=""><code>79ff6c7</code></a> Resolve interopability with spotless, lombok and VSCode</li>
<li>Additional commits viewable in <a href="https://github.com/diffplug/spotless/compare/maven/3.10.1...maven/3.10.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=com.diffplug.spotless:spotless-maven-plugin&package-manager=maven&previous-version=3.10.1&new-version=3.10.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eda229b12a28`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.