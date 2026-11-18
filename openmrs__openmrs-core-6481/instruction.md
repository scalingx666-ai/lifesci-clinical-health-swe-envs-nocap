# Issue

**Title:** maven(deps): bump com.diffplug.spotless:spotless-maven-plugin from 3.9.0 to 3.10.0

## Description

Bumps [com.diffplug.spotless:spotless-maven-plugin](https://github.com/diffplug/spotless) from 3.9.0 to 3.10.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/diffplug/spotless/releases">com.diffplug.spotless:spotless-maven-plugin's releases</a>.</em></p>
<blockquote>
<h2>Maven Plugin v3.10.0</h2>
<h3>Added</h3>
<ul>
<li>New <code>&lt;shortenFullyQualifiedTypes&gt;</code> step for Java, which replaces fully-qualified type names with their simple names and adds the imports they need. Best combined with <code>&lt;importOrder&gt;</code> and <code>&lt;removeUnusedImports&gt;</code>. (<a href="">#2945</a>)</li>
<li>Add embedded lockfiles to Eclipse JDT for every supported version (<code>4.9</code> through <code>4.40</code>), so <code>eclipse()</code> resolves from Maven Central instead of querying a P2 update site. Versions without an embedded lockfile still fall back to P2 provisioning. (<a href="">#1996</a>)</li>
<li>Add support to apply alternate license header within same format (<a href="">#872</a>)</li>
<li>Add support to skip license header application based on source file content pattern (<a href="">#650</a>).</li>
</ul>
<h3>Fixed</h3>
<ul>
<li><code>removeUnusedImports</code> no longer fails on Java <code>import module</code> declarations. (<a href="">#2890</a>)</li>
<li>Concurrent P2 provisioning no longer races Solstice's on-disk cache (affects Eclipse-based formatters under parallel builds). (<a href="">#3004</a>)</li>
</ul>
<h3>Changes</h3>
<ul>
<li>Default <code>google-java-format</code> remains <code>1.28.0</code> on JVM 17; bumps to <code>1.30.0</code> on JVM 21+; require at least <code>1.30.0</code> on JVM 25+ for <code>import module</code> support.</li>
<li>Bump default <code>eclipse</code> version to latest <code>4.39</code> -&gt; <code>4.40</code>. (<a href="">#1996</a>)</li>
<li>Document Maven skip properties <code>spotless.skip</code>, <code>spotless.check.skip</code>, and <code>spotless.apply.skip</code>. Goal-specific skips now live on their own mojos so they no longer leak across goals. (<a href="">#3009</a>)</li>
<li>Bump default <code>adocfmt</code> version <code>0.2.0</code> -&gt; <code>0.3.1</code>, which adds table formatting support (<code>&lt;formatTables&gt;</code>, <code>&lt;tableLayout&gt;</code>, <code>&lt;tableMaxLineWidth&gt;</code>, <code>&lt;tableBlankLines&gt;</code>).</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>426b21d</code></a> Published maven/3.10.0</li>
<li><a href=""><code>2fd42ea</code></a> Published gradle/8.10.0</li>
<li><a href=""><code>d71ed1a</code></a> Published lib/4.10.0</li>
<li><a href=""><code>8b57c01</code></a> Add shortenFullyQualifiedTypes step (fixes <a href="">#2945</a>) (<a href="">#3005</a> closes <a href="">#2945</a>)</li>
<li><a href=""><code>6b42c5e</code></a> fix: make the FQN-collecting visitor a named static class</li>
<li><a href=""><code>4430823</code></a> Better organization on the changelogs.</li>
<li><a href=""><code>45bea6d</code></a> Better place to put the shortenFullyQualifiedTypes docs</li>
<li><a href=""><code>0c49e65</code></a> chore: spotlessApply</li>
<li><a href=""><code>1c5bc0a</code></a> docs: list the Java import steps in the plugin README tables of contents</li>
<li><a href=""><code>cd57b58</code></a> docs: document shortenFullyQualifiedTypes in the plugin READMEs</li>
<li>Additional commits viewable in <a href="https://github.com/diffplug/spotless/compare/maven/3.9.0...maven/3.10.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=com.diffplug.spotless:spotless-maven-plugin&package-manager=maven&previous-version=3.9.0&new-version=3.10.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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