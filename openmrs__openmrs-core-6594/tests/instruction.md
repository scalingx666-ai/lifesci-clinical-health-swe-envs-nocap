# Issue

**Title:** maven(deps): bump hibernateVersion from 7.4.9.Final to 7.4.10.Final

## Description

Bumps `hibernateVersion` from 7.4.9.Final to 7.4.10.Final.
Updates `org.hibernate.orm:hibernate-core` from 7.4.9.Final to 7.4.10.Final
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/releases">org.hibernate.orm:hibernate-core's releases</a>.</em></p>
<blockquote>
<h2>Release 7.4.10</h2>
<h1>Hibernate ORM 7.4.10.Final released</h1>
<p>Today, we published a new release of Hibernate ORM 7.4: 7.4.10.Final.</p>
<p>You can find the full list of 7.4.10.Final changes <a href="https://hibernate.atlassian.net/issues/?jql=project%20%3D%20HHH%20AND%20fixVersion%20%3D%207.4.10">here</a>.</p>
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
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/blob/7.4.10/changelog.txt">org.hibernate.orm:hibernate-core's changelog</a>.</em></p>
<blockquote>
<h2>Changes in 7.4.10.Final (September 20, 2026)</h2>
<p><a href="https://hibernate.atlassian.net/projects/HHH/versions/40450">https://hibernate.atlassian.net/projects/HHH/versions/40450</a></p>
<p>** Bug
* HHH-20863 ActionQueue.clear() does not clear transactionCompletionCallbacks on rollback, causing HHH90010101
* HHH-20861 HHH100503 logged at INFO for normal constraint violation scenarios
* HHH-20857 Bug with <a href="https://github.com/Audited"><code>@​Audited</code></a>.Excluded and TABLE_PER_CLASS inheritance</p>
<p>** Improvement
* HHH-20883 mutation SQL should consistently include the tenant id</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>d946809</code></a> [Jenkins release job] Preparing release 7.4.10.Final</li>
<li><a href=""><code>44b5412</code></a> [Jenkins release job] changelog.txt updated by release build 7.4.10.Final</li>
<li><a href=""><code>3f4caa5</code></a> HHH-20861 HHH100503 logged at INFO for normal constraint violation scenarios</li>
<li><a href=""><code>75addda</code></a> HHH-20861 Add test for issue</li>
<li><a href=""><code>b8c12e8</code></a> HHH-20857 Fix runtime-generated pruned union subquery for type filters</li>
<li><a href=""><code>10677c4</code></a> HHH-20857 Fix TABLE_PER_CLASS audit excluded columns</li>
<li><a href=""><code>a7c5a6c</code></a> HHH-20863 ActionQueue.clear() does not clear transactionCompletionCallbacks o...</li>
<li><a href=""><code>934654f</code></a> HHH-20863 Add test for issue</li>
<li><a href=""><code>0330e11</code></a> HHH-20892 Add a test to verify that the issue is not present in this version.</li>
<li><a href=""><code>c644bb2</code></a> HHH-20883 Stabilize temporal tenant tests on Sybase</li>
<li>Additional commits viewable in <a href="https://github.com/hibernate/hibernate-orm/compare/7.4.9...7.4.10">compare view</a></li>
</ul>
</details>
<br />

Updates `org.hibernate.orm:hibernate-c3p0` from 7.4.9.Final to 7.4.10.Final
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/releases">org.hibernate.orm:hibernate-c3p0's releases</a>.</em></p>
<blockquote>
<h2>Release 7.4.10</h2>
<h1>Hibernate ORM 7.4.10.Final released</h1>
<p>Today, we published a new release of Hibernate ORM 7.4: 7.4.10.Final.</p>
<p>You can find the full list of 7.4.10.Final changes <a href="https://hibernate.atlassian.net/issues/?jql=project%20%3D%20HHH%20AND%20fixVersion%20%3D%207.4.10">here</a>.</p>
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
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/blob/7.4.10/changelog.txt">org.hibernate.orm:hibernate-c3p0's changelog</a>.</em></p>
<blockquote>
<h2>Changes in 7.4.10.Final (September 20, 2026)</h2>
<p><a href="https://hibernate.atlassian.net/projects/HHH/versions/40450">https://hibernate.atlassian.net/projects/HHH/versions/40450</a></p>
<p>** Bug
* HHH-20863 ActionQueue.clear() does not clear transactionCompletionCallbacks on rollback, causing HHH90010101
* HHH-20861 HHH100503 logged at INFO for normal constraint violation scenarios
* HHH-20857 Bug with <a href="https://github.com/Audited"><code>@​Audited</code></a>.Excluded and TABLE_PER_CLASS inheritance</p>
<p>** Improvement
* HHH-20883 mutation SQL should consistently include the tenant id</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>d946809</code></a> [Jenkins release job] Preparing release 7.4.10.Final</li>
<li><a href=""><code>44b5412</code></a> [Jenkins release job] changelog.txt updated by release build 7.4.10.Final</li>
<li><a href=""><code>3f4caa5</code></a> HHH-20861 HHH100503 logged at INFO for normal constraint violation scenarios</li>
<li><a href=""><code>75addda</code></a> HHH-20861 Add test for issue</li>
<li><a href=""><code>b8c12e8</code></a> HHH-20857 Fix runtime-generated pruned union subquery for type filters</li>
<li><a href=""><code>10677c4</code></a> HHH-20857 Fix TABLE_PER_CLASS audit excluded columns</li>
<li><a href=""><code>a7c5a6c</code></a> HHH-20863 ActionQueue.clear() does not clear transactionCompletionCallbacks o...</li>
<li><a href=""><code>934654f</code></a> HHH-20863 Add test for issue</li>
<li><a href=""><code>0330e11</code></a> HHH-20892 Add a test to verify that the issue is not present in this version.</li>
<li><a href=""><code>c644bb2</code></a> HHH-20883 Stabilize temporal tenant tests on Sybase</li>
<li>Additional commits viewable in <a href="https://github.com/hibernate/hibernate-orm/compare/7.4.9...7.4.10">compare view</a></li>
</ul>
</details>
<br />

Updates `org.hibernate.orm:hibernate-envers` from 7.4.9.Final to 7.4.10.Final
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/releases">org.hibernate.orm:hibernate-envers's releases</a>.</em></p>
<blockquote>
<h2>Release 7.4.10</h2>
<h1>Hibernate ORM 7.4.10.Final released</h1>
<p>Today, we published a new release of Hibernate ORM 7.4: 7.4.10.Final.</p>
<p>You can find the full list of 7.4.10.Final changes <a href="https://hibernate.atlassian.net/issues/?jql=project%20%3D%20HHH%20AND%20fixVersion%20%3D%207.4.10">here</a>.</p>
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
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/blob/7.4.10/changelog.txt">org.hibernate.orm:hibernate-envers's changelog</a>.</em></p>
<blockquote>
<h2>Changes in 7.4.10.Final (September 20, 2026)</h2>
<p><a href="https://hibernate.atlassian.net/projects/HHH/versions/40450">https://hibernate.atlassian.net/projects/HHH/versions/40450</a></p>
<p>** Bug
* HHH-20863 ActionQueue.clear() does not clear transactionCompletionCallbacks on rollback, causing HHH90010101
* HHH-20861 HHH100503 logged at INFO for normal constraint violation scenarios
* HHH-20857 Bug with <a href="https://github.com/Audited"><code>@​Audited</code></a>.Excluded and TABLE_PER_CLASS inheritance</p>
<p>** Improvement
* HHH-20883 mutation SQL should consistently include the tenant id</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>d946809</code></a> [Jenkins release job] Preparing release 7.4.10.Final</li>
<li><a href=""><code>44b5412</code></a> [Jenkins release job] changelog.txt updated by release build 7.4.10.Final</li>
<li><a href=""><code>3f4caa5</code></a> HHH-20861 HHH100503 logged at INFO for normal constraint violation scenarios</li>
<li><a href=""><code>75addda</code></a> HHH-20861 Add test for issue</li>
<li><a href=""><code>b8c12e8</code></a> HHH-20857 Fix runtime-generated pruned union subquery for type filters</li>
<li><a href=""><code>10677c4</code></a> HHH-20857 Fix TABLE_PER_CLASS audit excluded columns</li>
<li><a href=""><code>a7c5a6c</code></a> HHH-20863 ActionQueue.clear() does not clear transactionCompletionCallbacks o...</li>
<li><a href=""><code>934654f</code></a> HHH-20863 Add test for issue</li>
<li><a href=""><code>0330e11</code></a> HHH-20892 Add a test to verify that the issue is not present in this version.</li>
<li><a href=""><code>c644bb2</code></a> HHH-20883 Stabilize temporal tenant tests on Sybase</li>
<li>Additional commits viewable in <a href="https://github.com/hibernate/hibernate-orm/compare/7.4.9...7.4.10">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7aa1583e3ab0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.