# Issue

**Title:** maven(deps): bump com.diffplug.spotless:spotless-maven-plugin from 3.8.0 to 3.9.0

## Description

Bumps [com.diffplug.spotless:spotless-maven-plugin](https://github.com/diffplug/spotless) from 3.8.0 to 3.9.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/diffplug/spotless/releases">com.diffplug.spotless:spotless-maven-plugin's releases</a>.</em></p>
<blockquote>
<h2>Maven Plugin v3.9.0</h2>
<h3>Added</h3>
<ul>
<li>Add support for Java formatting via <a href="https://github.com/agustafson/prince-of-space"><code>prince-of-space</code></a> with the new <code>&lt;princeOfSpace&gt;</code> step. (<a href="">#2991</a>)</li>
</ul>
<h3>Changes</h3>
<ul>
<li>Replace RDF formatter library <code>de.atextor:turtle-formatter</code> (discontinued) with <code>cool.rdf:cool-rdf-formatter</code> (its new coordinates); the RDF/turtle formatter now requires Java 25+. (<a href="">#2995</a>)</li>
<li>Bump default <code>greclipse</code> version to latest <code>4.39</code> -&gt; <code>4.40</code>. (<a href="">#2989</a>)</li>
<li>Bump default <code>tabletest-formatter</code> version <code>1.1.1</code> -&gt; <code>1.1.2</code>.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>ff6ac27</code></a> Published maven/3.9.0</li>
<li><a href=""><code>cbd01c4</code></a> Published gradle/8.9.0</li>
<li><a href=""><code>c724e70</code></a> Published lib/4.9.0</li>
<li><a href=""><code>793638d</code></a> Replace de.atextor:turtle-formatter with cool.rdf:cool-rdf-formatter (<a href="">#2995</a>)</li>
<li><a href=""><code>3cb7227</code></a> Note Java 25+ requirement for RDF formatter; tidy changelogs</li>
<li><a href=""><code>fd9eb96</code></a> Merge remote-tracking branch 'origin/main' into use-cool-rdf-formatter</li>
<li><a href=""><code>d407109</code></a> Add support for prince-of-space Java formatter (<a href="">#2991</a>)</li>
<li><a href=""><code>cb64859</code></a> Merge remote-tracking branch 'origin/main' into use-cool-rdf-formatter</li>
<li><a href=""><code>f88db43</code></a> Bump tabletest-formatter to 1.1.2 (<a href="">#3001</a>)</li>
<li><a href=""><code>ec7db39</code></a> Bump tabletest-formatter to 1.1.2</li>
<li>Additional commits viewable in <a href="https://github.com/diffplug/spotless/compare/maven/3.8.0...maven/3.9.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=com.diffplug.spotless:spotless-maven-plugin&package-manager=maven&previous-version=3.8.0&new-version=3.9.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `58c1d9f3506e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.