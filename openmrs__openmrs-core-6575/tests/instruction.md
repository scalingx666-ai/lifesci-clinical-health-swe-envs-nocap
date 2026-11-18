# Issue

**Title:** maven(deps): bump hibernateVersion from 7.4.7.Final to 7.4.8.Final

## Description

Bumps `hibernateVersion` from 7.4.7.Final to 7.4.8.Final.
Updates `org.hibernate.orm:hibernate-core` from 7.4.7.Final to 7.4.8.Final
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/releases">org.hibernate.orm:hibernate-core's releases</a>.</em></p>
<blockquote>
<h2>Release 7.4.8</h2>
<h1>Hibernate ORM 7.4.8.Final released</h1>
<p>Today, we published a new release of Hibernate ORM 7.4: 7.4.8.Final.</p>
<p>You can find the full list of 7.4.8.Final changes <a href="https://hibernate.atlassian.net/issues/?jql=project%20%3D%20HHH%20AND%20fixVersion%20%3D%207.4.8">here</a>.</p>
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
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/blob/7.4.8/changelog.txt">org.hibernate.orm:hibernate-core's changelog</a>.</em></p>
<blockquote>
<h2>Changes in 7.4.8.Final (September 13, 2026)</h2>
<p><a href="https://hibernate.atlassian.net/projects/HHH/versions/40444">https://hibernate.atlassian.net/projects/HHH/versions/40444</a></p>
<p>** Bug
* HHH-20855 SQL Server temporal rounding causing trouble with sub-micro input values
* HHH-20849 org.hibernate.query.range.Range#suffix wrongly expects pattern
* HHH-20806 Join elimination in 7.x skips <a href="https://github.com/SQLRestriction"><code>@​SQLRestriction</code></a> when querying by to-one association id
* HHH-20805 MySQL schema update fails, if foreignkey related index is unique
* HHH-20804 StatefulPersistenceContext.clear() does not release newEntityHolder
* HHH-20801 AnyType.guessEntityPersister uses the wrapped proxy instead of the unwrapped implementation in its fallback → UnknownEntityTypeException during flush logging
* HHH-20782 <a href="https://github.com/FilterJoinTable"><code>@​FilterJoinTable</code></a> throws NPE when used with explicit HQL join
* HHH-20744 UnknownTableReferenceException when querying the non-owning side of a one-to-one-mapping with a pessimistic lock mode
* HHH-20675 <a href="https://github.com/FilterDef"><code>@​FilterDef</code></a>(applyToLoadByKey = true) breaks JOIN FETCH of a JOINED-inheritance to-one association: subclass table joins dropped from FROM while their columns remain in SELECT (invalid SQL)
* HHH-20632 Regression: UnknownTableReferenceException fetching an <a href="https://github.com/Any"><code>@​Any</code></a> discriminator through treat() (since 7.4.0, HHH-16730)
* HHH-20343 HTE (Bulk ID) temporary table ignores PhysicalNamingStrategy when using SequenceGenerator
* HHH-19486 SQLGrammarException when joining to subquery with Case expression
* HHH-19485 AssertionError when using Subquery with Case in Criteria API
* HHH-18911 Usage of ConcreteProxy in lazy loaded ManyToOne reference</p>
<p>** Deprecation
* HHH-20862 Deprecate reflection optimizer and related property access APIs</p>
<p>** Task
* HHH-20851 Upgrade to ant 1.10.18
* HHH-20848 Drop meaningless &quot;provided&quot; dependency to ant in hibernate-envers</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>2d3a7b8</code></a> [Jenkins release job] Preparing release 7.4.8.Final</li>
<li><a href=""><code>ca17983</code></a> [Jenkins release job] changelog.txt updated by release build 7.4.8.Final</li>
<li><a href=""><code>39d80c7</code></a> HHH-19486 Test and fix an alias collision for subquery in FROM clause select ...</li>
<li><a href=""><code>7e8f5df</code></a> HHH-19485 Fix FromClause#queryTableReferences potentially initializing a Lazy...</li>
<li><a href=""><code>c53a08c</code></a> HHH-19485 Fix TableReference#containsAffectedTableName exiting early</li>
<li><a href=""><code>418fd2d</code></a> HHH-19485 Reproduce assertion error when selecting case expression through FR...</li>
<li><a href=""><code>c39a73f</code></a> HHH-20862 Deprecate reflection optimizer and related property access APIs</li>
<li><a href=""><code>54c3cf0</code></a> HHH-20855 Fix SQL Server temporal rounding with sub-micro input values</li>
<li><a href=""><code>e66b6a5</code></a> HHH-20744 Skip inverse to-one attributes in follow-on locking</li>
<li><a href=""><code>b55bfc8</code></a> Don't use --illegal-field-mutation=deny in JDK 28 testing</li>
<li>Additional commits viewable in <a href="https://github.com/hibernate/hibernate-orm/compare/7.4.7...7.4.8">compare view</a></li>
</ul>
</details>
<br />

Updates `org.hibernate.orm:hibernate-c3p0` from 7.4.7.Final to 7.4.8.Final
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/releases">org.hibernate.orm:hibernate-c3p0's releases</a>.</em></p>
<blockquote>
<h2>Release 7.4.8</h2>
<h1>Hibernate ORM 7.4.8.Final released</h1>
<p>Today, we published a new release of Hibernate ORM 7.4: 7.4.8.Final.</p>
<p>You can find the full list of 7.4.8.Final changes <a href="https://hibernate.atlassian.net/issues/?jql=project%20%3D%20HHH%20AND%20fixVersion%20%3D%207.4.8">here</a>.</p>
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
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/blob/7.4.8/changelog.txt">org.hibernate.orm:hibernate-c3p0's changelog</a>.</em></p>
<blockquote>
<h2>Changes in 7.4.8.Final (September 13, 2026)</h2>
<p><a href="https://hibernate.atlassian.net/projects/HHH/versions/40444">https://hibernate.atlassian.net/projects/HHH/versions/40444</a></p>
<p>** Bug
* HHH-20855 SQL Server temporal rounding causing trouble with sub-micro input values
* HHH-20849 org.hibernate.query.range.Range#suffix wrongly expects pattern
* HHH-20806 Join elimination in 7.x skips <a href="https://github.com/SQLRestriction"><code>@​SQLRestriction</code></a> when querying by to-one association id
* HHH-20805 MySQL schema update fails, if foreignkey related index is unique
* HHH-20804 StatefulPersistenceContext.clear() does not release newEntityHolder
* HHH-20801 AnyType.guessEntityPersister uses the wrapped proxy instead of the unwrapped implementation in its fallback → UnknownEntityTypeException during flush logging
* HHH-20782 <a href="https://github.com/FilterJoinTable"><code>@​FilterJoinTable</code></a> throws NPE when used with explicit HQL join
* HHH-20744 UnknownTableReferenceException when querying the non-owning side of a one-to-one-mapping with a pessimistic lock mode
* HHH-20675 <a href="https://github.com/FilterDef"><code>@​FilterDef</code></a>(applyToLoadByKey = true) breaks JOIN FETCH of a JOINED-inheritance to-one association: subclass table joins dropped from FROM while their columns remain in SELECT (invalid SQL)
* HHH-20632 Regression: UnknownTableReferenceException fetching an <a href="https://github.com/Any"><code>@​Any</code></a> discriminator through treat() (since 7.4.0, HHH-16730)
* HHH-20343 HTE (Bulk ID) temporary table ignores PhysicalNamingStrategy when using SequenceGenerator
* HHH-19486 SQLGrammarException when joining to subquery with Case expression
* HHH-19485 AssertionError when using Subquery with Case in Criteria API
* HHH-18911 Usage of ConcreteProxy in lazy loaded ManyToOne reference</p>
<p>** Deprecation
* HHH-20862 Deprecate reflection optimizer and related property access APIs</p>
<p>** Task
* HHH-20851 Upgrade to ant 1.10.18
* HHH-20848 Drop meaningless &quot;provided&quot; dependency to ant in hibernate-envers</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>2d3a7b8</code></a> [Jenkins release job] Preparing release 7.4.8.Final</li>
<li><a href=""><code>ca17983</code></a> [Jenkins release job] changelog.txt updated by release build 7.4.8.Final</li>
<li><a href=""><code>39d80c7</code></a> HHH-19486 Test and fix an alias collision for subquery in FROM clause select ...</li>
<li><a href=""><code>7e8f5df</code></a> HHH-19485 Fix FromClause#queryTableReferences potentially initializing a Lazy...</li>
<li><a href=""><code>c53a08c</code></a> HHH-19485 Fix TableReference#containsAffectedTableName exiting early</li>
<li><a href=""><code>418fd2d</code></a> HHH-19485 Reproduce assertion error when selecting case expression through FR...</li>
<li><a href=""><code>c39a73f</code></a> HHH-20862 Deprecate reflection optimizer and related property access APIs</li>
<li><a href=""><code>54c3cf0</code></a> HHH-20855 Fix SQL Server temporal rounding with sub-micro input values</li>
<li><a href=""><code>e66b6a5</code></a> HHH-20744 Skip inverse to-one attributes in follow-on locking</li>
<li><a href=""><code>b55bfc8</code></a> Don't use --illegal-field-mutation=deny in JDK 28 testing</li>
<li>Additional commits viewable in <a href="https://github.com/hibernate/hibernate-orm/compare/7.4.7...7.4.8">compare view</a></li>
</ul>
</details>
<br />

Updates `org.hibernate.orm:hibernate-envers` from 7.4.7.Final to 7.4.8.Final
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/releases">org.hibernate.orm:hibernate-envers's releases</a>.</em></p>
<blockquote>
<h2>Release 7.4.8</h2>
<h1>Hibernate ORM 7.4.8.Final released</h1>
<p>Today, we published a new release of Hibernate ORM 7.4: 7.4.8.Final.</p>
<p>You can find the full list of 7.4.8.Final changes <a href="https://hibernate.atlassian.net/issues/?jql=project%20%3D%20HHH%20AND%20fixVersion%20%3D%207.4.8">here</a>.</p>
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
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/blob/7.4.8/changelog.txt">org.hibernate.orm:hibernate-envers's changelog</a>.</em></p>
<blockquote>
<h2>Changes in 7.4.8.Final (September 13, 2026)</h2>
<p><a href="https://hibernate.atlassian.net/projects/HHH/versions/40444">https://hibernate.atlassian.net/projects/HHH/versions/40444</a></p>
<p>** Bug
* HHH-20855 SQL Server temporal rounding causing trouble with sub-micro input values
* HHH-20849 org.hibernate.query.range.Range#suffix wrongly expects pattern
* HHH-20806 Join elimination in 7.x skips <a href="https://github.com/SQLRestriction"><code>@​SQLRestriction</code></a> when querying by to-one association id
* HHH-20805 MySQL schema update fails, if foreignkey related index is unique
* HHH-20804 StatefulPersistenceContext.clear() does not release newEntityHolder
* HHH-20801 AnyType.guessEntityPersister uses the wrapped proxy instead of the unwrapped implementation in its fallback → UnknownEntityTypeException during flush logging
* HHH-20782 <a href="https://github.com/FilterJoinTable"><code>@​FilterJoinTable</code></a> throws NPE when used with explicit HQL join
* HHH-20744 UnknownTableReferenceException when querying the non-owning side of a one-to-one-mapping with a pessimistic lock mode
* HHH-20675 <a href="https://github.com/FilterDef"><code>@​FilterDef</code></a>(applyToLoadByKey = true) breaks JOIN FETCH of a JOINED-inheritance to-one association: subclass table joins dropped from FROM while their columns remain in SELECT (invalid SQL)
* HHH-20632 Regression: UnknownTableReferenceException fetching an <a href="https://github.com/Any"><code>@​Any</code></a> discriminator through treat() (since 7.4.0, HHH-16730)
* HHH-20343 HTE (Bulk ID) temporary table ignores PhysicalNamingStrategy when using SequenceGenerator
* HHH-19486 SQLGrammarException when joining to subquery with Case expression
* HHH-19485 AssertionError when using Subquery with Case in Criteria API
* HHH-18911 Usage of ConcreteProxy in lazy loaded ManyToOne reference</p>
<p>** Deprecation
* HHH-20862 Deprecate reflection optimizer and related property access APIs</p>
<p>** Task
* HHH-20851 Upgrade to ant 1.10.18
* HHH-20848 Drop meaningless &quot;provided&quot; dependency to ant in hibernate-envers</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>2d3a7b8</code></a> [Jenkins release job] Preparing release 7.4.8.Final</li>
<li><a href=""><code>ca17983</code></a> [Jenkins release job] changelog.txt updated by release build 7.4.8.Final</li>
<li><a href=""><code>39d80c7</code></a> HHH-19486 Test and fix an alias collision for subquery in FROM clause select ...</li>
<li><a href=""><code>7e8f5df</code></a> HHH-19485 Fix FromClause#queryTableReferences potentially initializing a Lazy...</li>
<li><a href=""><code>c53a08c</code></a> HHH-19485 Fix TableReference#containsAffectedTableName exiting early</li>
<li><a href=""><code>418fd2d</code></a> HHH-19485 Reproduce assertion error when selecting case expression through FR...</li>
<li><a href=""><code>c39a73f</code></a> HHH-20862 Deprecate reflection optimizer and related property access APIs</li>
<li><a href=""><code>54c3cf0</code></a> HHH-20855 Fix SQL Server temporal rounding with sub-micro input values</li>
<li><a href=""><code>e66b6a5</code></a> HHH-20744 Skip inverse to-one attributes in follow-on locking</li>
<li><a href=""><code>b55bfc8</code></a> Don't use --illegal-field-mutation=deny in JDK 28 testing</li>
<li>Additional commits viewable in <a href="https://github.com/hibernate/hibernate-orm/compare/7.4.7...7.4.8">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9439adfe5b3d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.