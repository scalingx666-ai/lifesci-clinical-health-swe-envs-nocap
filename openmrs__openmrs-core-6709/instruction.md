# Issue

**Title:** maven(deps): bump org.hibernate.validator:hibernate-validator from 9.1.4.Final to 9.1.5.Final

## Description

Bumps [org.hibernate.validator:hibernate-validator](https://github.com/hibernate/hibernate-validator) from 9.1.4.Final to 9.1.5.Final.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-validator/releases">org.hibernate.validator:hibernate-validator's releases</a>.</em></p>
<blockquote>
<h2>Release 9.1.5.Final</h2>
<h1>Hibernate Validator 9.1.5.Final released</h1>
<p>We are pleased to announce the release of Hibernate Validator 9.1: 9.1.5.Final.</p>
<p>You can find the full list of 9.1.5.Final changes <a href="https://hibernate.atlassian.net/issues/?jql=project%20%3D%20HV%20AND%20fixVersion%20%3D%209.1.5.Final">here</a>.</p>
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
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-validator/blob/9.1.5.Final/changelog.md">org.hibernate.validator:hibernate-validator's changelog</a>.</em></p>
<blockquote>
<h2>9.1.5.Final (2026-10-13)</h2>
<p><a href="https://hibernate.atlassian.net/projects/HV/versions/40454">Full changelog</a></p>
<h3>Bug</h3>
<ul>
<li><a href="https://hibernate.atlassian.net/browse/HV-2256">HV-2256</a> - addMessageParameter fix</li>
</ul>
<h3>Improvement</h3>
<ul>
<li><a href="https://hibernate.atlassian.net/browse/HV-2263">HV-2263</a> - Bump joda-time to 2.14.4</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>257c5b8</code></a> [Jenkins release job] Preparing release 9.1.5.Final</li>
<li><a href=""><code>79140b6</code></a> [Jenkins release job] changelog.md updated by release build 9.1.5.Final</li>
<li><a href=""><code>3c73c34</code></a> [Jenkins release job] README.md updated by release build 9.1.5.Final</li>
<li><a href=""><code>188fa51</code></a> HV-2256 Add updates to migration guide/what's new doc</li>
<li><a href=""><code>f4ddf9e</code></a> HV-2256 Escape message parameters by default</li>
<li><a href=""><code>f0b26b8</code></a> [9.1] Bump the build-dependencies group across 1 directory with 4 updates</li>
<li><a href=""><code>668c038</code></a> Bump joda-time to 2.14.4 HV-2263</li>
<li><a href=""><code>3b87bf0</code></a> [9.1] Bump org.hibernate.infra:hibernate-asciidoctor-theme</li>
<li><a href=""><code>8d8cc71</code></a> [9.1] Bump org.asciidoctor:asciidoctorj-pdf</li>
<li><a href=""><code>5c8ca50</code></a> [Jenkins release job] Preparing next development iteration</li>
<li>See full diff in <a href="https://github.com/hibernate/hibernate-validator/compare/9.1.4.Final...9.1.5.Final">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.hibernate.validator:hibernate-validator&package-manager=maven&previous-version=9.1.4.Final&new-version=9.1.5.Final)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d4348493a005`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.