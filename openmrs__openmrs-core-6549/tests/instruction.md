# Issue

**Title:** maven(deps): bump org.apache.maven.plugins:maven-surefire-plugin from 3.5.6 to 3.6.0

## Description

Bumps [org.apache.maven.plugins:maven-surefire-plugin](https://github.com/apache/maven-surefire) from 3.5.6 to 3.6.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/apache/maven-surefire/releases">org.apache.maven.plugins:maven-surefire-plugin's releases</a>.</em></p>
<blockquote>
<h2>3.6.0</h2>
<!-- raw HTML omitted -->
<p>Please refer to the main page for what's new <a href="https://maven.apache.org/surefire/">https://maven.apache.org/surefire/</a>
And the migration page <a href="https://maven.apache.org/surefire/maven-surefire-plugin/whats-new-3-6-0.html">https://maven.apache.org/surefire/maven-surefire-plugin/whats-new-3-6-0.html</a></p>
<h2>🚀 New features and improvements</h2>
<ul>
<li>Fix <a href="">#3303</a>: distinguish JUnit 6 ParameterizedClass invocations (<a href="">#3432</a>) <a href="https://github.com/AzazelSensei"><code>@​AzazelSensei</code></a></li>
<li><a href="https://issues.apache.org/jira/browse/SUREFIRE-1639">[SUREFIRE-1639]</a> - Add ability to configure JUnit 5 TestExecutionListener (<a href="">#3438</a>) <a href="https://github.com/pan3793"><code>@​pan3793</code></a></li>
<li>Issue <a href="">#838</a> Implement extension point to run diagnosis tools when forked JVM times out (<a href="">#3372</a>) <a href="https://github.com/olamy"><code>@​olamy</code></a></li>
<li><a href="https://issues.apache.org/jira/browse/SUREFIRE-2148">[SUREFIRE-2148]</a> - Verify recovered BeforeAll does not fail build (<a href="">#3419</a>) <a href="https://github.com/wilx"><code>@​wilx</code></a></li>
<li><a href="https://issues.apache.org/jira/browse/SUREFIRE-823">[SUREFIRE-823]</a> - Decouple -DskipTests from Failsafe plugin (<a href="">#3371</a>) <a href="https://github.com/olamy"><code>@​olamy</code></a></li>
<li>Use StackWalker in StackTraceProvider when available (Java 9+) (<a href="">#3374</a>) <a href="https://github.com/olamy"><code>@​olamy</code></a></li>
<li>[Issue-3380] Send sourceQualifiedName to forked clients (<a href="">#3380</a>) (<a href="">#3381</a>) <a href="https://github.com/fabriciorby"><code>@​fabriciorby</code></a></li>
</ul>
<h2>🐛 Bug Fixes</h2>
<ul>
<li><a href="https://issues.apache.org/jira/browse/SUREFIRE-523">[SUREFIRE-523]</a> - Link all reported tests to source XRef (<a href="">#3445</a>) <a href="https://github.com/wilx"><code>@​wilx</code></a></li>
<li><a href="https://issues.apache.org/jira/browse/SUREFIRE-3446">[SUREFIRE-3446]</a> - Fix direct selection of JUnit Jupiter <a href="https://github.com/Nested"><code>@​Nested</code></a> classes (<a href="">#3447</a>) <a href="https://github.com/wilx"><code>@​wilx</code></a></li>
<li>Discover tests in a fork when a toolchain JDK is used (<a href="">#3444</a>) <a href="https://github.com/olamy"><code>@​olamy</code></a></li>
<li>[SUREFIRE-2239, SUREFIRE-2241, SUREFIRE-2260, SUREFIRE-2274, SUREFIRE-2300] Preserve JUnit Platform test identity across reruns (<a href="">#3418</a>) <a href="https://github.com/wilx"><code>@​wilx</code></a></li>
<li>Fix <a href="">#3428</a>: resolve parents via TestPlan.getParent for pre-1.8 platforms (<a href="">#3429</a>) <a href="https://github.com/kalayciburak"><code>@​kalayciburak</code></a></li>
<li><a href="https://issues.apache.org/jira/browse/SUREFIRE-859">[SUREFIRE-859]</a> - Make random test order reproducible (<a href="">#3421</a>) <a href="https://github.com/wilx"><code>@​wilx</code></a></li>
<li>[SUREFIRE-862, SUREFIRE-3178] Handle missing Failsafe summary files (<a href="">#3417</a>) <a href="https://github.com/wilx"><code>@​wilx</code></a></li>
<li>fix: report AfterAll/AfterClass exceptions as errors again (<a href="">#3412</a>) (<a href="">#3413</a>) <a href="https://github.com/arimu1"><code>@​arimu1</code></a></li>
<li>Fixes <a href="">#3264</a> : tests inside <a href="https://github.com/Suite"><code>@​Suite</code></a> incorrectly classified as flakes (<a href="">#3342</a>) <a href="https://github.com/mirkoalicastro"><code>@​mirkoalicastro</code></a></li>
<li>Fix Windows flake in CommandChannelDecoderTest (<a href="">#3400</a>) <a href="https://github.com/ascheman"><code>@​ascheman</code></a></li>
<li>Fix reportNameSuffix in XML testcase classname (<a href="">#3379</a>) <a href="https://github.com/goutamadwant"><code>@​goutamadwant</code></a></li>
<li>Fix: resolve relative classpath elements against the fork's working dir (<a href="">#3333</a>) <a href="https://github.com/cwegener-79"><code>@​cwegener-79</code></a></li>
</ul>
<h2>📝 Documentation updates</h2>
<ul>
<li>Magnify the home, well at least have something rather than nothing :) (<a href="">#3377</a>) <a href="https://github.com/olamy"><code>@​olamy</code></a></li>
<li>Restore the straight quotes the FAQ conversion turned typographic (<a href="">#3425</a>) <a href="https://github.com/slachiewicz"><code>@​slachiewicz</code></a></li>
<li>Restore the table borders lost in the APT conversion (<a href="">#3424</a>) <a href="https://github.com/slachiewicz"><code>@​slachiewicz</code></a></li>
<li>Convert the FAQ from FML to Markdown (<a href="">#3423</a>) <a href="https://github.com/slachiewicz"><code>@​slachiewicz</code></a></li>
<li>Convert the remaining site documentation from APT to Markdown (<a href="">#3422</a>) <a href="https://github.com/slachiewicz"><code>@​slachiewicz</code></a></li>
<li>javadoc: clarify statelessTestsetReporter, consoleOutputReporter, (<a href="">#3410</a>) <a href="https://github.com/joshinii"><code>@​joshinii</code></a></li>
<li>Add AGENTS.md + SECURITY.md security-model pointer for scanner discoverability (<a href="">#3387</a>) <a href="https://github.com/potiuk"><code>@​potiuk</code></a></li>
<li>Update documentation we support Junit 6 as well :) (<a href="">#3370</a>) <a href="https://github.com/olamy"><code>@​olamy</code></a></li>
</ul>
<h2>👻 Maintenance</h2>
<ul>
<li>Stop dependabot from updating test fixtures (<a href="">#3440</a>) <a href="https://github.com/slachiewicz"><code>@​slachiewicz</code></a></li>
<li>Migrate legacy plugin Javadoc annotations (<a href="">#3416</a>) <a href="https://github.com/wilx"><code>@​wilx</code></a></li>
<li>Use the resolver's own HTTP transport in the report plugin tests (<a href="">#3414</a>) <a href="https://github.com/slachiewicz"><code>@​slachiewicz</code></a></li>
<li>Pin maven-jar-plugin 3.5.1 in modular IT fixtures (<a href="">#3398</a>) <a href="https://github.com/ascheman"><code>@​ascheman</code></a></li>
<li>Add AGENTS.md + SECURITY.md security-model pointer for scanner discoverability (<a href="">#3387</a>) <a href="https://github.com/potiuk"><code>@​potiuk</code></a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>0ff622b</code></a> [maven-release-plugin] prepare release surefire-3.6.0</li>
<li><a href=""><code>bb3932a</code></a> Let's go for 3.6.0 release</li>
<li><a href=""><code>3002a16</code></a> Bump mavenVersion from 3.9.14 to 3.9.16</li>
<li><a href=""><code>61a531d</code></a> Bump Maven parent version from 47 to 49 (<a href="">#3449</a>)</li>
<li><a href=""><code>e52ead4</code></a> [SUREFIRE-523] Link all reported tests to source XRef (<a href="">#3445</a>)</li>
<li><a href=""><code>45102fa</code></a> [SUREFIRE-3446] Fix direct selection of JUnit Jupiter <a href="https://github.com/Nested"><code>@​Nested</code></a> classes (<a href="">#3447</a>)</li>
<li><a href=""><code>b2e1f70</code></a> Fix <a href="">#3303</a>: distinguish JUnit 6 ParameterizedClass invocations (<a href="">#3432</a>)</li>
<li><a href=""><code>c051938</code></a> Discover tests in a fork when a toolchain JDK is used (<a href="">#3444</a>)</li>
<li><a href=""><code>db75df8</code></a> Bump org.codehaus.plexus:plexus-java from 1.5.2 to 1.6.0 (<a href="">#3441</a>)</li>
<li><a href=""><code>77f2759</code></a> Bump org.codehaus.plexus:plexus-interpolation from 1.29 to 1.30.0</li>
<li>Additional commits viewable in <a href="https://github.com/apache/maven-surefire/compare/surefire-3.5.6...surefire-3.6.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.apache.maven.plugins:maven-surefire-plugin&package-manager=maven&previous-version=3.5.6&new-version=3.6.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `24946d82274e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.