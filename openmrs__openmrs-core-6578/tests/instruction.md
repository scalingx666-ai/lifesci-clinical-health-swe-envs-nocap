# Issue

**Title:** maven(deps): bump org.apache.maven.plugins:maven-deploy-plugin from 3.1.4 to 3.2.0

## Description

Bumps [org.apache.maven.plugins:maven-deploy-plugin](https://github.com/apache/maven-deploy-plugin) from 3.1.4 to 3.2.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/apache/maven-deploy-plugin/releases">org.apache.maven.plugins:maven-deploy-plugin's releases</a>.</em></p>
<blockquote>
<h2>3.2.0</h2>
<!-- raw HTML omitted -->
<h2>🚀 New features and improvements</h2>
<ul>
<li>Cache projectsWithDeployExecution to fix O(N²) reactor scan (<a href="">#697</a>) <a href="https://github.com/slawekjaranowski"><code>@​slawekjaranowski</code></a></li>
</ul>
<h2>🐛 Bug Fixes</h2>
<ul>
<li>Backport security audit fixes to 3.x (f004-f008, f010, f012) (<a href="">#701</a>) <a href="https://github.com/gnodet"><code>@​gnodet</code></a></li>
</ul>
<h2>📝 Documentation updates</h2>
<ul>
<li>Clarify deploy without editing this projects POM (<a href="">#694</a>) <a href="https://github.com/slawekjaranowski"><code>@​slawekjaranowski</code></a></li>
<li>Restore the plain form of the ASF licence header (<a href="">#688</a>) <a href="https://github.com/slachiewicz"><code>@​slachiewicz</code></a></li>
<li>Add AGENTS.md + SECURITY.md security-model pointer for scanner discoverability (<a href="">#674</a>) <a href="https://github.com/potiuk"><code>@​potiuk</code></a></li>
</ul>
<h2>👻 Maintenance</h2>
<ul>
<li>Simplify remote repository creation (<a href="">#696</a>) <a href="https://github.com/slawekjaranowski"><code>@​slawekjaranowski</code></a></li>
<li>Restore the plain form of the ASF licence header (<a href="">#688</a>) <a href="https://github.com/slachiewicz"><code>@​slachiewicz</code></a></li>
<li>enable build with Maven 4 (<a href="">#655</a>) <a href="https://github.com/hboutemy"><code>@​hboutemy</code></a></li>
<li>Add AGENTS.md + SECURITY.md security-model pointer for scanner discoverability (<a href="">#674</a>) <a href="https://github.com/potiuk"><code>@​potiuk</code></a></li>
<li>Migration to JUnit 5 - avoid using AbstractMojoTestCase (<a href="">#643</a>) <a href="https://github.com/slawekjaranowski"><code>@​slawekjaranowski</code></a></li>
<li>Migration to JUnit 5 - avoid using AbstractMojoTestCase in DeployFileMojoTest (<a href="">#629</a>) <a href="https://github.com/slawekjaranowski"><code>@​slawekjaranowski</code></a></li>
<li>Bump m-invoker-p to 3.9.1 (<a href="">#627</a>) <a href="https://github.com/slachiewicz"><code>@​slachiewicz</code></a></li>
<li>Feature/apt to md 3.x (<a href="">#620</a>) <a href="https://github.com/kwin"><code>@​kwin</code></a></li>
</ul>
<h2>🔧 Build</h2>
<ul>
<li>update deployAtEnd ITs to match latest 4 behaviour (<a href="">#667</a>) <a href="https://github.com/hboutemy"><code>@​hboutemy</code></a></li>
</ul>
<h2>📦 Dependency updates</h2>
<ul>
<li>Bump apache/maven-gh-actions-shared/.github/workflows/release-drafter.yml from 4 to 5 (<a href="">#681</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump apache/maven-gh-actions-shared/.github/workflows/maven-verify.yml from 4 to 5 (<a href="">#679</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump apache/maven-gh-actions-shared/.github/workflows/pr-automation.yml from 4 to 5 (<a href="">#680</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump org.apache.maven.plugins:maven-plugins from 48 to 49 (<a href="">#671</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump mavenVersion from 3.9.15 to 3.9.16 (<a href="">#665</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump org.apache.maven.plugins:maven-plugins from 47 to 48 (<a href="">#662</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump mavenVersion from 3.9.14 to 3.9.15 (<a href="">#657</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump mavenVersion from 3.9.13 to 3.9.14 (<a href="">#654</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump mavenVersion from 3.9.12 to 3.9.13 (<a href="">#648</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump resolverVersion from 1.9.26 to 1.9.27 (<a href="">#646</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump resolverVersion from 1.9.25 to 1.9.26 (<a href="">#642</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump org.apache.maven.plugin-testing:maven-plugin-testing-harness from 3.5.0 to 3.5.1 (<a href="">#640</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump org.apache.maven.plugins:maven-plugins from 46 to 47 (<a href="">#639</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump org.apache.maven.plugin-testing:maven-plugin-testing-harness from 3.4.0 to 3.5.0 (<a href="">#637</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump org.apache.maven.plugins:maven-plugins from 45 to 46 (<a href="">#636</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump mavenVersion from 3.9.11 to 3.9.12 (<a href="">#634</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump resolverVersion from 1.9.24 to 1.9.25 (<a href="">#631</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>7aab9fb</code></a> [maven-release-plugin] prepare release maven-deploy-plugin-3.2.0</li>
<li><a href=""><code>1f3eef5</code></a> Backport security audit fixes to 3.x (f004-f008, f010, f012)</li>
<li><a href=""><code>307f328</code></a> Simplify remote repository creation</li>
<li><a href=""><code>7b1bbc4</code></a> Cache projectsWithDeployExecution to fix O(N²) reactor scan</li>
<li><a href=""><code>a9177c6</code></a> Clarify deploy without editing this projects POM</li>
<li><a href=""><code>7c40513</code></a> Restore the plain form of the ASF licence header</li>
<li><a href=""><code>5969234</code></a> Update Release Drafter configuration to use custom tag template and remove un...</li>
<li><a href=""><code>df7b3fa</code></a> Bump apache/maven-gh-actions-shared/.github/workflows/release-drafter.yml</li>
<li><a href=""><code>b4e8aed</code></a> work around Maven 4 CLI lack of interpolation</li>
<li><a href=""><code>d634bb4</code></a> enable build with Maven 4</li>
<li>Additional commits viewable in <a href="https://github.com/apache/maven-deploy-plugin/compare/maven-deploy-plugin-3.1.4...maven-deploy-plugin-3.2.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.apache.maven.plugins:maven-deploy-plugin&package-manager=maven&previous-version=3.1.4&new-version=3.2.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `51c5652b5fe8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.