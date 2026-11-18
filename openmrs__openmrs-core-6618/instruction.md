# Issue

**Title:** maven(deps): bump com.diffplug.spotless:spotless-maven-plugin from 3.10.2 to 3.10.3

## Description

Bumps [com.diffplug.spotless:spotless-maven-plugin](https://github.com/diffplug/spotless) from 3.10.2 to 3.10.3.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/diffplug/spotless/releases">com.diffplug.spotless:spotless-maven-plugin's releases</a>.</em></p>
<blockquote>
<h2>Maven Plugin v3.10.3</h2>
<h3>Changes</h3>
<ul>
<li>Generate formatter defaults from version catalog. (<a href="">#3045</a>)</li>
<li>Bump default <code>gson</code> version <code>2.13.2</code> -&gt; <code>2.14.0</code>. (<a href="">#3045</a>)</li>
<li>Bump default <code>zjsonpatch</code> version <code>0.4.14</code> -&gt; <code>0.4.16</code>. (<a href="">#3045</a>)</li>
<li>Bump default <code>jackson-dataformat-yaml</code> version <code>2.14.1</code> -&gt; <code>2.20.1</code>. (<a href="">#3045</a>)</li>
<li>Bump default <code>ktfmt</code> version <code>0.63</code> -&gt; <code>0.64</code>. (<a href="">2988</a>)</li>
<li>Bump default <code>cleanthat</code> version <code>2.25</code> -&gt; <code>2.26</code>. (<a href="">#2882</a>)</li>
<li>Bump default <code>jackson</code> version <code>2.20.1</code> -&gt; <code>2.22.2</code>. (<a href="">#2819</a>)</li>
<li>Bump default <code>javaparser</code> version <code>3.27.1</code> -&gt; <code>3.28.2</code>. (<a href="">#3065</a>)</li>
<li>Bump default <code>palantir-java-format</code> version <code>2.80.0</code> -&gt; <code>2.98.0</code>. (<a href="">#3068</a>)</li>
<li>Bump default <code>scalafmt</code> version <code>3.8.1</code> -&gt; <code>3.11.5</code>. (<a href="">#2173</a>)</li>
<li>Bump default <code>google-java-format</code> version <code>1.30.0</code> -&gt; <code>1.36.1</code>. (<a href="">#3075</a>)</li>
<li>Bump default <code>gherkin-utils</code> version <code>10.0.0</code> -&gt; <code>12.0.2</code>. (<a href="">#2979</a>)</li>
</ul>
<h3>Fixed</h3>
<ul>
<li>Fix release signing by using Gradle's required eight-digit signing subkey ID. (<a href="">#3105</a>)</li>
<li>Fix race when creating the npm install cache directory. ((<a href="">#3096</a>)</li>
<li>GrEclipse no longer emits expected OSGi and nested-jar warnings during initialization. (<a href="">#2445</a>)</li>
<li><code>typescript</code> <code>prettier()</code> no longer emits a warning when its parser is already set to <code>typescript</code>. (<a href="">#3098</a>)</li>
<li><code>&lt;versionCatalog&gt;</code> preserves standalone comments at section boundaries and the end of the file. (<a href="">#3048</a>)</li>
<li><code>&lt;versionCatalog&gt;</code> preserves entries when comments contain unmatched brackets, preserves commas inside quoted strings, and keeps significant line boundaries in multiline entries. (<a href="">#3042</a>)</li>
<li><code>&lt;versionCatalog&gt;</code> now reports unfinished entries as lints at their starting line. These fail formatting by default, so upgrading may expose catalog errors that previously caused silent data loss. (<a href="">#3042</a>)</li>
<li>Eclipse JDT formatter step no longer fails with <code>NoClassDefFoundError</code> or <code>NoSuchMethodError</code> when lombok is active as a JVM agent (e.g. <code>-javaagent:lombok.jar</code> in Eclipse/VS Code/Cursor). (<a href="">#2795</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>61e2016</code></a> Published maven/3.10.3</li>
<li><a href=""><code>49e0b07</code></a> Published lib/4.10.3</li>
<li><a href=""><code>b7a7748</code></a> Fix release signing key ID format (<a href="">#3105</a>)</li>
<li><a href=""><code>be8005a</code></a> Document release signing correction (<a href="">#3105</a>)</li>
<li><a href=""><code>073fe61</code></a> Use short signing subkey ID for release publishing</li>
<li><a href=""><code>8ac44c7</code></a> Fix race when creating the npm install cache directory (<a href="">#3096</a>)</li>
<li><a href=""><code>3f2d955</code></a> Update dependency org.slf4j:slf4j-api to v2.0.20 (<a href="">#3100</a>)</li>
<li><a href=""><code>0c70ca8</code></a> Merge branch 'main' into fix/npm-cache-directory-race</li>
<li><a href=""><code>bbf44a4</code></a> Fix GrEclipse initialization warnings (<a href="">#3097</a>)</li>
<li><a href=""><code>b6bdcd0</code></a> Update dependency org.slf4j:slf4j-api to v2.0.20</li>
<li>Additional commits viewable in <a href="https://github.com/diffplug/spotless/compare/maven/3.10.2...maven/3.10.3">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=com.diffplug.spotless:spotless-maven-plugin&package-manager=maven&previous-version=3.10.2&new-version=3.10.3)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1222cf828bae`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.