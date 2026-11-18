# Issue

**Title:** maven(deps): bump hibernateVersion from 7.4.10.Final to 7.4.11.Final

## Description

Bumps `hibernateVersion` from 7.4.10.Final to 7.4.11.Final.
Updates `org.hibernate.orm:hibernate-core` from 7.4.10.Final to 7.4.11.Final
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/releases">org.hibernate.orm:hibernate-core's releases</a>.</em></p>
<blockquote>
<h2>Release 7.4.11</h2>
<h1>Hibernate ORM 7.4.11.Final released</h1>
<p>Today, we published a new release of Hibernate ORM 7.4: 7.4.11.Final.</p>
<p>You can find the full list of 7.4.11.Final changes <a href="https://hibernate.atlassian.net/issues/?jql=project%20%3D%20HHH%20AND%20fixVersion%20%3D%207.4.11">here</a>.</p>
<h2>What's new</h2>
<ul>
<li>See the <a href="https://hibernate.org/orm/releases/7.4">website</a> for requirements and compatibilities.</li>
<li>See the <a href="https://docs.hibernate.org/orm/7.4/whats-new/whats-new.html">What's New</a> guide for details about new features and capabilities.</li>
<li>See the <a href="https://docs.hibernate.org/orm/7.4/migration-guide/">Migration Guide</a> for details about migration.</li>
</ul>
<h2>Conclusion</h2>
<p>For additional details, see:</p>
<ul>
<li>the <a href="https://hibernate.org/orm/releases/7.4/">release page</a></li>
<li>the <a href="https://docs.hibernate.org/orm/7.4/migration-guide/">Migration Guide</a></li>
<li>the <a href="https://docs.hibernate.org/orm/7.4/introduction/html_single/">Introduction Guide</a></li>
<li>the <a href="https://docs.hibernate.org/orm/7.4/userguide/html_single/">User Guide</a></li>
<li>the <a href="https://docs.hibernate.org/orm/7.4/javadocs">API docs</a></li>
</ul>
<p>See also the following resources related to supported APIs:</p>
<ul>
<li>the <a href="https://hibernate.org/community/compatibility-policy/">compatibility policy</a></li>
<li>the <a href="https://docs.hibernate.org/orm/7.4/incubating/incubating.txt">incubating API report</a> (<code>@Incubating</code>)</li>
<li>the <a href="https://docs.hibernate.org/orm/7.4/deprecated/deprecated.txt">deprecated API report</a> (<code>@Deprecated</code> + <code>@Remove</code>)</li>
<li>the <a href="https://docs.hibernate.org/orm/7.4/internals/internal.txt">internal API report</a> (internal packages, <code>@Internal</code>)</li>
</ul>
<p>Visit the <a href="https://hibernate.org/community/">website</a> for details on getting in touch with us.</p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/blob/7.4.11/changelog.txt">org.hibernate.orm:hibernate-core's changelog</a>.</em></p>
<blockquote>
<h2>Changes in 7.4.11.Final (September 27, 2026)</h2>
<p><a href="https://hibernate.atlassian.net/projects/HHH/versions/40453">https://hibernate.atlassian.net/projects/HHH/versions/40453</a></p>
<p>** Bug
* HHH-20894 StatelessSession upsert and upsertMultiple concurrency problem
* HHH-20876 StatelessSession: Interceptor#onLoad isn't called
* HHH-20826 Emit MERGE for on conflict do nothing on H2, Oracle, and SQL Server instead of silently dropping the conflict clause
* HHH-17020 Can't use enum as string in join column when field is part of composite primary key</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>a95dd44</code></a> [Jenkins release job] Preparing release 7.4.11.Final</li>
<li><a href=""><code>bb72fdf</code></a> [Jenkins release job] changelog.txt updated by release build 7.4.11.Final</li>
<li><a href=""><code>7134c72</code></a> Switch maven-plugin intTest logging from logback to log4j2</li>
<li><a href=""><code>97efe59</code></a> Fix Maven plugin integration tests not falling back to Maven Central</li>
<li><a href=""><code>dd4001e</code></a> Fix Informix nightly failures</li>
<li><a href=""><code>58e974a</code></a> HHH-17020 Test and fix issues with enum in id-class not copying type related ...</li>
<li><a href=""><code>bc7d0fb</code></a> HHH-18910/HHH-17020 Test and fix issues with binding discriminator through pr...</li>
<li><a href=""><code>3cdebc0</code></a> HHH-20826 Prefer merge for conflict do-nothing to reduce constraint violation...</li>
<li><a href=""><code>4555ed0</code></a> HHH-20894 Ensure upsert/insert-or-update really is executed and retry batch p...</li>
<li><a href=""><code>57c59cf</code></a> HHH-20894 Make Sybase behave like a sane SQL database</li>
<li>Additional commits viewable in <a href="https://github.com/hibernate/hibernate-orm/compare/7.4.10...7.4.11">compare view</a></li>
</ul>
</details>
<br />

Updates `org.hibernate.orm:hibernate-c3p0` from 7.4.10.Final to 7.4.11.Final
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/releases">org.hibernate.orm:hibernate-c3p0's releases</a>.</em></p>
<blockquote>
<h2>Release 7.4.11</h2>
<h1>Hibernate ORM 7.4.11.Final released</h1>
<p>Today, we published a new release of Hibernate ORM 7.4: 7.4.11.Final.</p>
<p>You can find the full list of 7.4.11.Final changes <a href="https://hibernate.atlassian.net/issues/?jql=project%20%3D%20HHH%20AND%20fixVersion%20%3D%207.4.11">here</a>.</p>
<h2>What's new</h2>
<ul>
<li>See the <a href="https://hibernate.org/orm/releases/7.4">website</a> for requirements and compatibilities.</li>
<li>See the <a href="https://docs.hibernate.org/orm/7.4/whats-new/whats-new.html">What's New</a> guide for details about new features and capabilities.</li>
<li>See the <a href="https://docs.hibernate.org/orm/7.4/migration-guide/">Migration Guide</a> for details about migration.</li>
</ul>
<h2>Conclusion</h2>
<p>For additional details, see:</p>
<ul>
<li>the <a href="https://hibernate.org/orm/releases/7.4/">release page</a></li>
<li>the <a href="https://docs.hibernate.org/orm/7.4/migration-guide/">Migration Guide</a></li>
<li>the <a href="https://docs.hibernate.org/orm/7.4/introduction/html_single/">Introduction Guide</a></li>
<li>the <a href="https://docs.hibernate.org/orm/7.4/userguide/html_single/">User Guide</a></li>
<li>the <a href="https://docs.hibernate.org/orm/7.4/javadocs">API docs</a></li>
</ul>
<p>See also the following resources related to supported APIs:</p>
<ul>
<li>the <a href="https://hibernate.org/community/compatibility-policy/">compatibility policy</a></li>
<li>the <a href="https://docs.hibernate.org/orm/7.4/incubating/incubating.txt">incubating API report</a> (<code>@Incubating</code>)</li>
<li>the <a href="https://docs.hibernate.org/orm/7.4/deprecated/deprecated.txt">deprecated API report</a> (<code>@Deprecated</code> + <code>@Remove</code>)</li>
<li>the <a href="https://docs.hibernate.org/orm/7.4/internals/internal.txt">internal API report</a> (internal packages, <code>@Internal</code>)</li>
</ul>
<p>Visit the <a href="https://hibernate.org/community/">website</a> for details on getting in touch with us.</p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/blob/7.4.11/changelog.txt">org.hibernate.orm:hibernate-c3p0's changelog</a>.</em></p>
<blockquote>
<h2>Changes in 7.4.11.Final (September 27, 2026)</h2>
<p><a href="https://hibernate.atlassian.net/projects/HHH/versions/40453">https://hibernate.atlassian.net/projects/HHH/versions/40453</a></p>
<p>** Bug
* HHH-20894 StatelessSession upsert and upsertMultiple concurrency problem
* HHH-20876 StatelessSession: Interceptor#onLoad isn't called
* HHH-20826 Emit MERGE for on conflict do nothing on H2, Oracle, and SQL Server instead of silently dropping the conflict clause
* HHH-17020 Can't use enum as string in join column when field is part of composite primary key</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>a95dd44</code></a> [Jenkins release job] Preparing release 7.4.11.Final</li>
<li><a href=""><code>bb72fdf</code></a> [Jenkins release job] changelog.txt updated by release build 7.4.11.Final</li>
<li><a href=""><code>7134c72</code></a> Switch maven-plugin intTest logging from logback to log4j2</li>
<li><a href=""><code>97efe59</code></a> Fix Maven plugin integration tests not falling back to Maven Central</li>
<li><a href=""><code>dd4001e</code></a> Fix Informix nightly failures</li>
<li><a href=""><code>58e974a</code></a> HHH-17020 Test and fix issues with enum in id-class not copying type related ...</li>
<li><a href=""><code>bc7d0fb</code></a> HHH-18910/HHH-17020 Test and fix issues with binding discriminator through pr...</li>
<li><a href=""><code>3cdebc0</code></a> HHH-20826 Prefer merge for conflict do-nothing to reduce constraint violation...</li>
<li><a href=""><code>4555ed0</code></a> HHH-20894 Ensure upsert/insert-or-update really is executed and retry batch p...</li>
<li><a href=""><code>57c59cf</code></a> HHH-20894 Make Sybase behave like a sane SQL database</li>
<li>Additional commits viewable in <a href="https://github.com/hibernate/hibernate-orm/compare/7.4.10...7.4.11">compare view</a></li>
</ul>
</details>
<br />

Updates `org.hibernate.orm:hibernate-envers` from 7.4.10.Final to 7.4.11.Final
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/releases">org.hibernate.orm:hibernate-envers's releases</a>.</em></p>
<blockquote>
<h2>Release 7.4.11</h2>
<h1>Hibernate ORM 7.4.11.Final released</h1>
<p>Today, we published a new release of Hibernate ORM 7.4: 7.4.11.Final.</p>
<p>You can find the full list of 7.4.11.Final changes <a href="https://hibernate.atlassian.net/issues/?jql=project%20%3D%20HHH%20AND%20fixVersion%20%3D%207.4.11">here</a>.</p>
<h2>What's new</h2>
<ul>
<li>See the <a href="https://hibernate.org/orm/releases/7.4">website</a> for requirements and compatibilities.</li>
<li>See the <a href="https://docs.hibernate.org/orm/7.4/whats-new/whats-new.html">What's New</a> guide for details about new features and capabilities.</li>
<li>See the <a href="https://docs.hibernate.org/orm/7.4/migration-guide/">Migration Guide</a> for details about migration.</li>
</ul>
<h2>Conclusion</h2>
<p>For additional details, see:</p>
<ul>
<li>the <a href="https://hibernate.org/orm/releases/7.4/">release page</a></li>
<li>the <a href="https://docs.hibernate.org/orm/7.4/migration-guide/">Migration Guide</a></li>
<li>the <a href="https://docs.hibernate.org/orm/7.4/introduction/html_single/">Introduction Guide</a></li>
<li>the <a href="https://docs.hibernate.org/orm/7.4/userguide/html_single/">User Guide</a></li>
<li>the <a href="https://docs.hibernate.org/orm/7.4/javadocs">API docs</a></li>
</ul>
<p>See also the following resources related to supported APIs:</p>
<ul>
<li>the <a href="https://hibernate.org/community/compatibility-policy/">compatibility policy</a></li>
<li>the <a href="https://docs.hibernate.org/orm/7.4/incubating/incubating.txt">incubating API report</a> (<code>@Incubating</code>)</li>
<li>the <a href="https://docs.hibernate.org/orm/7.4/deprecated/deprecated.txt">deprecated API report</a> (<code>@Deprecated</code> + <code>@Remove</code>)</li>
<li>the <a href="https://docs.hibernate.org/orm/7.4/internals/internal.txt">internal API report</a> (internal packages, <code>@Internal</code>)</li>
</ul>
<p>Visit the <a href="https://hibernate.org/community/">website</a> for details on getting in touch with us.</p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/blob/7.4.11/changelog.txt">org.hibernate.orm:hibernate-envers's changelog</a>.</em></p>
<blockquote>
<h2>Changes in 7.4.11.Final (September 27, 2026)</h2>
<p><a href="https://hibernate.atlassian.net/projects/HHH/versions/40453">https://hibernate.atlassian.net/projects/HHH/versions/40453</a></p>
<p>** Bug
* HHH-20894 StatelessSession upsert and upsertMultiple concurrency problem
* HHH-20876 StatelessSession: Interceptor#onLoad isn't called
* HHH-20826 Emit MERGE for on conflict do nothing on H2, Oracle, and SQL Server instead of silently dropping the conflict clause
* HHH-17020 Can't use enum as string in join column when field is part of composite primary key</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>a95dd44</code></a> [Jenkins release job] Preparing release 7.4.11.Final</li>
<li><a href=""><code>bb72fdf</code></a> [Jenkins release job] changelog.txt updated by release build 7.4.11.Final</li>
<li><a href=""><code>7134c72</code></a> Switch maven-plugin intTest logging from logback to log4j2</li>
<li><a href=""><code>97efe59</code></a> Fix Maven plugin integration tests not falling back to Maven Central</li>
<li><a href=""><code>dd4001e</code></a> Fix Informix nightly failures</li>
<li><a href=""><code>58e974a</code></a> HHH-17020 Test and fix issues with enum in id-class not copying type related ...</li>
<li><a href=""><code>bc7d0fb</code></a> HHH-18910/HHH-17020 Test and fix issues with binding discriminator through pr...</li>
<li><a href=""><code>3cdebc0</code></a> HHH-20826 Prefer merge for conflict do-nothing to reduce constraint violation...</li>
<li><a href=""><code>4555ed0</code></a> HHH-20894 Ensure upsert/insert-or-update really is executed and retry batch p...</li>
<li><a href=""><code>57c59cf</code></a> HHH-20894 Make Sybase behave like a sane SQL database</li>
<li>Additional commits viewable in <a href="https://github.com/hibernate/hibernate-orm/compare/7.4.10...7.4.11">compare view</a></li>
</ul>
</details>
<br />

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d801de9eb121`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.