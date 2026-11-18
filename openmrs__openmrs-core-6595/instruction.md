# Issue

**Title:** maven(deps): bump org.hibernate.validator:hibernate-validator from 9.1.3.Final to 9.1.4.Final

## Description

Bumps [org.hibernate.validator:hibernate-validator](https://github.com/hibernate/hibernate-validator) from 9.1.3.Final to 9.1.4.Final.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-validator/releases">org.hibernate.validator:hibernate-validator's releases</a>.</em></p>
<blockquote>
<h2>Release 9.1.4.Final</h2>
<h1>Hibernate Validator 9.1.4.Final released</h1>
<p>We are pleased to announce the release of Hibernate Validator 9.1: 9.1.4.Final.</p>
<p>You can find the full list of 9.1.4.Final changes <a href="https://hibernate.atlassian.net/issues/?jql=project%20%3D%20HV%20AND%20fixVersion%20%3D%209.1.4.Final">here</a>.</p>
<h2>What's new</h2>
<ul>
<li>See the <a href="https://hibernate.org/validator/releases/9.1">website</a> for requirements and compatibilities.</li>
<li>See the <a href="https://docs.hibernate.org/validator/9.1/whats-new/en-US/html_single/">What's New</a> guide for details about new features and capabilities.</li>
</ul>
<h2>Conclusion</h2>
<p>For additional details, see:</p>
<ul>
<li>the <a href="https://hibernate.org/validator/releases/9.1/">release page</a></li>
<li>the <a href="https://docs.hibernate.org/validator/9.1/migration-guide/">Migration Guide</a></li>
<li>the <a href="https://docs.hibernate.org/validator/9.1/reference/en-US/html_single/#validator-gettingstarted">Getting started</a></li>
<li>the <a href="https://docs.hibernate.org/validator/9.1/reference/en-US/html_single/">Reference Guide</a></li>
<li>the <a href="https://docs.hibernate.org/validator/9.1/api">API docs</a></li>
</ul>
<p>Visit the <a href="https://hibernate.org/community/">website</a> for details on getting in touch with us.</p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-validator/blob/9.1.4.Final/changelog.md">org.hibernate.validator:hibernate-validator's changelog</a>.</em></p>
<blockquote>
<h2>9.1.4.Final (2026-09-20)</h2>
<p><a href="https://hibernate.atlassian.net/projects/HV/versions/40268">Full changelog</a></p>
<h3>Bug</h3>
<ul>
<li><a href="https://hibernate.atlassian.net/browse/HV-2253">HV-2253</a> - ClassNotFoundException thrown when an EL implementation and OSGi are not on the class path</li>
</ul>
<h3>Improvement</h3>
<ul>
<li><a href="https://hibernate.atlassian.net/browse/HV-2243">HV-2243</a> - Bump joda-time to 2.14.3</li>
<li><a href="https://hibernate.atlassian.net/browse/HV-2242">HV-2242</a> - Update to OpenJFX to 17.0.20</li>
</ul>
<h3>Task</h3>
<ul>
<li><a href="https://hibernate.atlassian.net/browse/HV-2244">HV-2244</a> - Tune the content of javadoc jars to reduce the size of files published to Maven Central</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>5504b0c</code></a> [Jenkins release job] Preparing release 9.1.4.Final</li>
<li><a href=""><code>1306aab</code></a> [Jenkins release job] changelog.md updated by release build 9.1.4.Final</li>
<li><a href=""><code>715cbdb</code></a> [Jenkins release job] README.md updated by release build 9.1.4.Final</li>
<li><a href=""><code>84e8d2e</code></a> HV-2253 When determining the Jakarta Expression Language implementation, igno...</li>
<li><a href=""><code>f3002a3</code></a> [9.1] Bump org.codehaus.mojo:build-helper-maven-plugin</li>
<li><a href=""><code>971d85b</code></a> [9.1] Bump the build-dependencies group with 3 updates</li>
<li><a href=""><code>dcb1305</code></a> Tune the content of javadoc jars to reduce the size of files published to Mav...</li>
<li><a href=""><code>d01ed37</code></a> [9.1] Bump version.org.apache.groovy from 5.0.7 to 5.0.8</li>
<li><a href=""><code>6023258</code></a> Bump joda-time to 2.14.3 HV-2243</li>
<li><a href=""><code>3db152e</code></a> Update to OpenJFX to 17.0.20 HV-2242</li>
<li>Additional commits viewable in <a href="https://github.com/hibernate/hibernate-validator/compare/9.1.3.Final...9.1.4.Final">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.hibernate.validator:hibernate-validator&package-manager=maven&previous-version=9.1.3.Final&new-version=9.1.4.Final)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7aa1583e3ab0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.