# Issue

**Title:** maven(deps): bump com.diffplug.spotless:spotless-maven-plugin from 3.10.3 to 3.10.4

## Description

Bumps [com.diffplug.spotless:spotless-maven-plugin](https://github.com/diffplug/spotless) from 3.10.3 to 3.10.4.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/diffplug/spotless/releases">com.diffplug.spotless:spotless-maven-plugin's releases</a>.</em></p>
<blockquote>
<h2>Maven Plugin v3.10.4</h2>
<h3>Changes</h3>
<ul>
<li>Bump default <code>eclipse</code> version from <code>4.40</code> to <code>4.41</code>.</li>
<li>Bump default <code>gherkin</code> version <code>42.0.0</code> -&gt; <code>42.0.1</code>. (<a href="">#3088</a>)</li>
<li>Bump default <code>jackson</code> version <code>2.22.2</code> -&gt; <code>2.22.3</code>. (<a href="">#3101</a>)</li>
<li>Bump default <code>palantir-java-format</code> version <code>2.98.0</code> -&gt; <code>2.102.0</code>. (<a href="">#3103</a>, <a href="">#3132</a>)</li>
<li>Bump default <code>mockito-core</code> version <code>5.23.0</code> -&gt; <code>5.24.0</code>. (<a href="">#3106</a>)</li>
<li>Bump default <code>greclipse</code> version to latest <code>4.40</code> -&gt; <code>4.41</code>. (<a href="">#3123</a>)</li>
<li>Bump default <code>ktfmt</code> version <code>0.64</code> -&gt; <code>0.65</code>. (<a href="">#3135</a>)<br />
Which moved to the <code>org.jetbrains.kotlinx:ktfmt</code> coordinate and <code>org.jetbrains.kotlinx.ktfmt</code> package. Older versions are still supported.</li>
<li>Bump default <code>palantir-java-format</code> version <code>2.99.0</code> -&gt; <code>2.102.0</code>. (<a href="">#3132</a>)</li>
</ul>
<h3>Fixed</h3>
<ul>
<li>Migrate Plexus component injection to JSR-330 and Maven parameter. (<a href="">#3122</a>)</li>
<li><code>shortenFullyQualifiedTypes</code> leaves a qualified name alone when the enclosing type extends or implements a type that is not in the same file, so an inherited member type cannot take the simple name. (<a href="">#3117</a>)</li>
<li><code>expandWildcardImports</code> no longer drops the import of a type that is only used to qualify a static member (such as <code>Collections.sort(list)</code> or <code>TimeUnit.SECONDS</code>), or the static import of a field or enum constant (such as <code>PI</code> from <code>import static java.lang.Math.*</code>), which produced code that did not compile. (<a href="">#2833</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>62e727d</code></a> Published maven/3.10.4</li>
<li><a href=""><code>d9e7a41</code></a> Published gradle/8.10.4</li>
<li><a href=""><code>c006d66</code></a> Published lib/4.10.4</li>
<li><a href=""><code>8adb835</code></a> Merge release publishing fixes into main (<a href="">#3138</a>)</li>
<li><a href=""><code>67b4dbf</code></a> Remove internal publishing changes from release notes</li>
<li><a href=""><code>b9c4830</code></a> Keep Rewrite plugin on publicly resolvable releases (<a href="">#3036</a>)</li>
<li><a href=""><code>1c93df4</code></a> Update dependency com.palantir.javaformat:palantir-java-format to v2.102.0 (#...</li>
<li><a href=""><code>ab153a9</code></a> Keep Rewrite plugin on publicly resolvable releases</li>
<li><a href=""><code>feb10d8</code></a> Update plugin rewrite to v7.41.0</li>
<li><a href=""><code>2083664</code></a> Update changelogs for default formatter version bump (<a href="">#3132</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/diffplug/spotless/compare/maven/3.10.3...maven/3.10.4">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=com.diffplug.spotless:spotless-maven-plugin&package-manager=maven&previous-version=3.10.3&new-version=3.10.4)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `453679a52fce`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.