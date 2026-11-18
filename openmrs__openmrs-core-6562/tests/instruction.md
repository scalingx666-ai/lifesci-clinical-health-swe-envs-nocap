# Issue

**Title:** maven(deps-dev): bump org.sonarsource.scanner.maven:sonar-maven-plugin from 5.7.0.6970 to 5.8.0.7211

## Description

Bumps [org.sonarsource.scanner.maven:sonar-maven-plugin](https://github.com/SonarSource/sonar-scanner-maven) from 5.7.0.6970 to 5.8.0.7211.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/SonarSource/sonar-scanner-maven/releases">org.sonarsource.scanner.maven:sonar-maven-plugin's releases</a>.</em></p>
<blockquote>
<h2>5.8.0.7211</h2>
<h1>Release notes - Sonar Scanner for Maven - 5.8</h1>
<h3>Maintenance</h3>
<p><a href="https://sonarsource.atlassian.net/browse/SCANMAVEN-382">SCANMAVEN-382</a> Prepare next development iteration 5.8.0</p>
<p><a href="https://sonarsource.atlassian.net/browse/SCANMAVEN-384">SCANMAVEN-384</a> Fix QG broken by the new testing rules</p>
<p><a href="https://sonarsource.atlassian.net/browse/SCANMAVEN-385">SCANMAVEN-385</a> Code Quality reorganization from jvm to CI Experience Squad</p>
<p><a href="https://sonarsource.atlassian.net/browse/SCANMAVEN-386">SCANMAVEN-386</a> ToggleLockBranch: Add additional-message</p>
<p><a href="https://sonarsource.atlassian.net/browse/SCANMAVEN-387">SCANMAVEN-387</a> Code Quality Slack channel reorganization</p>
<p><a href="https://sonarsource.atlassian.net/browse/SCANMAVEN-390">SCANMAVEN-390</a> Upgrade orchestrator to version 6.3.0</p>
<p><a href="https://sonarsource.atlassian.net/browse/SCANMAVEN-392">SCANMAVEN-392</a> Upgrade jetty test dependencies to version 9.4.58.v20250814</p>
<p><a href="https://sonarsource.atlassian.net/browse/SCANMAVEN-395">SCANMAVEN-395</a> Remove scheduled invocation of sonar:sonar shorthand test</p>
<p><a href="https://sonarsource.atlassian.net/browse/SCANMAVEN-397">SCANMAVEN-397</a> Replace Maven 4.0.0-rc-5 in ITs with Maven 4.0.0-rc-6</p>
<p><a href="https://sonarsource.atlassian.net/browse/SCANMAVEN-398">SCANMAVEN-398</a> Upgrade orchestrator to version 6.4.0</p>
<p><a href="https://sonarsource.atlassian.net/browse/SCANMAVEN-399">SCANMAVEN-399</a> Update sonar-scanner-java-library to 4.1.2.1663</p>
<p><a href="https://sonarsource.atlassian.net/browse/SCANMAVEN-401">SCANMAVEN-401</a> Upgrade Jetty used by e2e tests</p>
<p><a href="https://sonarsource.atlassian.net/browse/SCANMAVEN-402">SCANMAVEN-402</a> Upgrade orchestrator to version 6.4.3.4676</p>
<h3>Feature</h3>
<p><a href="https://sonarsource.atlassian.net/browse/SCANMAVEN-403">SCANMAVEN-403</a> Releasability status fails on property-dump-plugin version</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>7347a92</code></a> SCANMAVEN-403 Releasability status fails on property-dump-plugin version (<a href="">#426</a>)</li>
<li><a href=""><code>002f55c</code></a> SCANMAVEN-402 Upgrade orchestrator to version 6.4.3.4676 (<a href="">#425</a>)</li>
<li><a href=""><code>fc7515f</code></a> SCANMAVEN-401 Upgrade Jetty used by e2e tests (<a href="">#424</a>)</li>
<li><a href=""><code>16dedb3</code></a> SCANMAVEN-399 Update sonar-scanner-java-library to 4.1.2.1663 (<a href="">#421</a>)</li>
<li><a href=""><code>ad81956</code></a> SCANMAVEN-397 Upgrade Maven 4 to 4.0.0-rc-6 in tests (<a href="">#420</a>)</li>
<li><a href=""><code>86e9516</code></a> SCANMAVEN-398 Upgrade orchestrator to version 6.4.0 (<a href="">#419</a>)</li>
<li><a href=""><code>c26335c</code></a> SCANMAVEN-395 Remove scheduled invocation of sonar:sonar shorthand test (<a href="">#417</a>)</li>
<li><a href=""><code>6a79ca6</code></a> SCANMAVEN-392 Upgrade jetty test dependencies to version 9.4.58.v20250814 (<a href="">#416</a>)</li>
<li><a href=""><code>57bb131</code></a> SCANMAVEN-390 Upgrade orchestrator to version 6.3.0 (<a href="">#414</a>)</li>
<li><a href=""><code>9d50b6d</code></a> GHA-355 Add statuses: write permission for release-lock feature (<a href="">#412</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/SonarSource/sonar-scanner-maven/compare/5.7.0.6970...5.8.0.7211">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.sonarsource.scanner.maven:sonar-maven-plugin&package-manager=maven&previous-version=5.7.0.6970&new-version=5.8.0.7211)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `006171d832b8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.