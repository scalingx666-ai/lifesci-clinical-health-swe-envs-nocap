# Issue

**Title:** maven(deps): bump org.apache.maven.plugins:maven-compiler-plugin from 3.15.0 to 3.16.0

## Description

Bumps [org.apache.maven.plugins:maven-compiler-plugin](https://github.com/apache/maven-compiler-plugin) from 3.15.0 to 3.16.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/apache/maven-compiler-plugin/releases">org.apache.maven.plugins:maven-compiler-plugin's releases</a>.</em></p>
<blockquote>
<h2>3.16.0</h2>
<!-- raw HTML omitted -->
<h2>🚀 New features and improvements</h2>
<ul>
<li>Recompile when dependencies change (<a href="">#1102</a>) <a href="https://github.com/wilx"><code>@​wilx</code></a></li>
<li>Fix incremental detection of empty sources, 3.x (<a href="">#1075</a>) <a href="https://github.com/wilx"><code>@​wilx</code></a></li>
</ul>
<h2>🐛 Bug Fixes</h2>
<ul>
<li><a href="https://issues.apache.org/jira/browse/MCOMPILER-578">[MCOMPILER-578]</a> - Track outputs across compiler executions (<a href="">#1091</a>) <a href="https://github.com/wilx"><code>@​wilx</code></a></li>
<li>Build fails when annotation processor list is empty (but present) (<a href="">#1077</a>) <a href="https://github.com/wilx"><code>@​wilx</code></a></li>
<li><a href="https://issues.apache.org/jira/browse/MCOMPILER-374">[MCOMPILER-374]</a> - Unable to compile MR-JAR code against older directories when module-info.java is present (<a href="">#1093</a>) <a href="https://github.com/wilx"><code>@​wilx</code></a></li>
<li>Make mcompiler-120 IT locale independent (<a href="">#1063</a>) <a href="https://github.com/anilvdl"><code>@​anilvdl</code></a></li>
</ul>
<h2>📝 Documentation updates</h2>
<ul>
<li><a href="https://issues.apache.org/jira/browse/MCOMPILER-569">[MCOMPILER-569]</a> - Document implicitly compiled excluded sources (<a href="">#1092</a>) <a href="https://github.com/wilx"><code>@​wilx</code></a></li>
<li>Add AGENTS.md + SECURITY.md security-model pointer for scanner discoverability (<a href="">#1074</a>) <a href="https://github.com/potiuk"><code>@​potiuk</code></a></li>
</ul>
<h2>👻 Maintenance</h2>
<ul>
<li>Avoid using deprecated method CompilerConfiguration.setCompilerVersion (<a href="">#1121</a>) <a href="https://github.com/slawekjaranowski"><code>@​slawekjaranowski</code></a></li>
<li>Replace adopt-openj9 by semeru JDK distribution on GH (<a href="">#1122</a>) <a href="https://github.com/slawekjaranowski"><code>@​slawekjaranowski</code></a></li>
<li>Port the site documentation from APT to Markdown (<a href="">#1110</a>) <a href="https://github.com/slachiewicz"><code>@​slachiewicz</code></a></li>
<li>Verify against Maven 4.0.0-rc-6 (<a href="">#1105</a>) <a href="https://github.com/slachiewicz"><code>@​slachiewicz</code></a></li>
<li>Fix tests on Jenkins (<a href="">#1100</a>) <a href="https://github.com/slawekjaranowski"><code>@​slawekjaranowski</code></a></li>
<li>Add AGENTS.md + SECURITY.md security-model pointer for scanner discoverability (<a href="">#1074</a>) <a href="https://github.com/potiuk"><code>@​potiuk</code></a></li>
<li>Refactor compiler mojo to use dependency injection and improve string… (<a href="">#1066</a>) <a href="https://github.com/slachiewicz"><code>@​slachiewicz</code></a></li>
<li>Fix ITs for Maven 3.10.x (<a href="">#1061</a>) <a href="https://github.com/slawekjaranowski"><code>@​slawekjaranowski</code></a></li>
<li>Update maven-surefire-plugin version to 3.x in the MCOMPILER-481 IT (<a href="">#1035</a>) <a href="https://github.com/cdouillard"><code>@​cdouillard</code></a></li>
</ul>
<h2>📦 Dependency updates</h2>
<ul>
<li>Bump plexusCompilerVersion from 2.16.2 to 2.17.0 (<a href="">#1112</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump org.codehaus.plexus:plexus-java from 1.5.2 to 1.6.0 (<a href="">#1113</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>use latest Maven 4 (<a href="">#1045</a>) <a href="https://github.com/hboutemy"><code>@​hboutemy</code></a></li>
<li>Bump apache/maven-gh-actions-shared/.github/workflows/release-drafter.yml from 4 to 5 (<a href="">#1083</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump apache/maven-gh-actions-shared/.github/workflows/pr-automation.yml from 4 to 5 (<a href="">#1082</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump apache/maven-gh-actions-shared/.github/workflows/maven-verify.yml from 4 to 5 (<a href="">#1084</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump org.apache.maven.plugins:maven-plugins from 48 to 49 (<a href="">#1068</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump org.apache.maven.plugins:maven-invoker-plugin from 3.9.1 to 3.10.1 (<a href="">#1047</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump org.apache.maven.plugins:maven-plugins from 47 to 48 (<a href="">#1050</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump mavenVersion from 3.9.14 to 3.9.16 (<a href="">#1054</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump org.ow2.asm:asm from 9.10 to 9.10.1 (<a href="">#1059</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump org.ow2.asm:asm from 9.9.1 to 9.10 (<a href="">#1053</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump mavenVersion from 3.9.13 to 3.9.14 (<a href="">#1041</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump mavenVersion from 3.9.12 to 3.9.13 (<a href="">#1038</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump org.apache.maven.plugin-testing:maven-plugin-testing-harness from 3.5.0 to 3.5.1 (<a href="">#1032</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>e7bba6e</code></a> [maven-release-plugin] prepare release maven-compiler-plugin-3.16.0</li>
<li><a href=""><code>c906809</code></a> Avoid using deprecated method CompilerConfiguration.setCompilerVersion</li>
<li><a href=""><code>ad74fee</code></a> Replace adopt-openj9 by semeru JDK distribution on GH</li>
<li><a href=""><code>beb0eda</code></a> Recompile when dependencies change (<a href="">#1102</a>)</li>
<li><a href=""><code>a0b689e</code></a> [MCOMPILER-578] Track outputs across compiler executions (<a href="">#1091</a>)</li>
<li><a href=""><code>2e81228</code></a> Fix incremental detection of empty sources, 3.x (<a href="">#1075</a>)</li>
<li><a href=""><code>2132f5b</code></a> configure ATR project</li>
<li><a href=""><code>5992b77</code></a> Build fails when annotation processor list is empty (but present) (<a href="">#1077</a>)</li>
<li><a href=""><code>acccef7</code></a> Bump plexusCompilerVersion from 2.16.2 to 2.17.0</li>
<li><a href=""><code>72bc445</code></a> Bump org.codehaus.plexus:plexus-java from 1.5.2 to 1.6.0</li>
<li>Additional commits viewable in <a href="https://github.com/apache/maven-compiler-plugin/compare/maven-compiler-plugin-3.15.0...maven-compiler-plugin-3.16.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.apache.maven.plugins:maven-compiler-plugin&package-manager=maven&previous-version=3.15.0&new-version=3.16.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `28e3bab9e206`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.