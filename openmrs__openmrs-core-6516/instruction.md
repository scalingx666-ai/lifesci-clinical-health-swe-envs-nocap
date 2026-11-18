# Issue

**Title:** maven(deps): bump hibernateVersion from 7.4.5.Final to 7.4.6.Final

## Description

Bumps `hibernateVersion` from 7.4.5.Final to 7.4.6.Final.
Updates `org.hibernate.orm:hibernate-core` from 7.4.5.Final to 7.4.6.Final
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/releases">org.hibernate.orm:hibernate-core's releases</a>.</em></p>
<blockquote>
<h2>Release 7.4.6</h2>
<h1>Hibernate ORM 7.4.6.Final released</h1>
<p>Today, we published a new release of Hibernate ORM 7.4: 7.4.6.Final.</p>
<p>You can find the full list of 7.4.6.Final changes <a href="https://hibernate.atlassian.net/issues/?jql=project%20%3D%20HHH%20AND%20fixVersion%20%3D%207.4.6">here</a>.</p>
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
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/blob/7.4.6/changelog.txt">org.hibernate.orm:hibernate-core's changelog</a>.</em></p>
<blockquote>
<h2>Changes in 7.4.6.Final (August 23, 2026)</h2>
<p><a href="https://hibernate.atlassian.net/projects/HHH/versions/40133">https://hibernate.atlassian.net/projects/HHH/versions/40133</a></p>
<p>** Bug
* HHH-20788 [Quarkus 3.20.5 / Hibernate ORM 6.6.40.Final] quarkus.otel.logs.enabled=true fails SessionFactory build for TABLE_PER_CLASS collections
* HHH-20783 hibernate.transactions{result=&quot;failure&quot;} metric can transiently go negative due to non-atomic counter reads, breaking the whole Prometheus scrape on Micrometer 1.14+
* HHH-20779 Envers: unwrap proxies in collection-change audit work units
* HHH-20776 CriteriaBuilder.literal() mistypes an enum constant declared with a class body
* HHH-20772 ARRAY_AGG column in Jakarta Data query method cannot be mapped to result type property
* HHH-20743 <code>hibernate-maven-plugin</code> <code>enhance</code> goal computes wrong class names when <code>fileSets</code> directory differs from <code>classesDirectory</code>
* HHH-20707 Missing import for inner interface type in CDI accessor metamodel methods
* HHH-20696 Implicit name of list index columns not applied by MetadataBuilder
* HHH-20661 HQL UNION fails when unioning java.util.Date from different attribute paths
* HHH-20624 StackOverflowError when creating entity manager with attribute converter hierarchy with generic parameter
* HHH-20515 Adjust default for SessionCheckMode on Session.findMultiple()
* HHH-20472 Generated metamodel class missing <code>List</code> import
* HHH-20452 <a href="https://github.com/OneToMany"><code>@​OneToMany</code></a> mapping silently dropped when orm.xml contributes a partial overlay (entity-listeners only) to an entity whose <a href="https://github.com/Id"><code>@​Id</code></a> is inherited from a <a href="https://github.com/MappedSuperclass"><code>@​MappedSuperclass</code></a>
* HHH-20438 Basic-array body predicates fail with AssertionError from SqmMappingModelHelper.resolveSqmPath
* HHH-20348 <code>DataException</code> / <code>ClassCastException</code> when aggregating primitive</p>
<p>** Task
* HHH-20736 Tune the content of javadocs to reduce the size of files published to Maven Central
* HHH-20710 Update to hibernate-models 1.1.2</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>43e2e9a</code></a> [Jenkins release job] Preparing release 7.4.6.Final</li>
<li><a href=""><code>cd34e60</code></a> [Jenkins release job] changelog.txt updated by release build 7.4.6.Final</li>
<li><a href=""><code>229571c</code></a> HHH-20710 Add test for generic Map subtype resolution with JSON mapping</li>
<li><a href=""><code>de419ce</code></a> HHH-20710 Update to hibernate-models 1.1.2</li>
<li><a href=""><code>284a4be</code></a> HHH-20788 Return null for TablePerSubclass and clarify informational nature o...</li>
<li><a href=""><code>f74ba58</code></a> Make testsuite fit for JDK 28 Valhalla preview</li>
<li><a href=""><code>33465fe</code></a> Add JDK 28 to the testing JDK list</li>
<li><a href=""><code>5e398fd</code></a> Skip some tests causing nightly failures on MySQL due to a bug</li>
<li><a href=""><code>cf53ffa</code></a> HHH-20783 Add a dedicated failed-transactions counter to Statistics</li>
<li><a href=""><code>f4e0be3</code></a> HHH-20772 add <a href="https://github.com/Incubating"><code>@​Incubating</code></a> to new Processor options</li>
<li>Additional commits viewable in <a href="https://github.com/hibernate/hibernate-orm/compare/7.4.5...7.4.6">compare view</a></li>
</ul>
</details>
<br />

Updates `org.hibernate.orm:hibernate-c3p0` from 7.4.5.Final to 7.4.6.Final
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/releases">org.hibernate.orm:hibernate-c3p0's releases</a>.</em></p>
<blockquote>
<h2>Release 7.4.6</h2>
<h1>Hibernate ORM 7.4.6.Final released</h1>
<p>Today, we published a new release of Hibernate ORM 7.4: 7.4.6.Final.</p>
<p>You can find the full list of 7.4.6.Final changes <a href="https://hibernate.atlassian.net/issues/?jql=project%20%3D%20HHH%20AND%20fixVersion%20%3D%207.4.6">here</a>.</p>
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
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/blob/7.4.6/changelog.txt">org.hibernate.orm:hibernate-c3p0's changelog</a>.</em></p>
<blockquote>
<h2>Changes in 7.4.6.Final (August 23, 2026)</h2>
<p><a href="https://hibernate.atlassian.net/projects/HHH/versions/40133">https://hibernate.atlassian.net/projects/HHH/versions/40133</a></p>
<p>** Bug
* HHH-20788 [Quarkus 3.20.5 / Hibernate ORM 6.6.40.Final] quarkus.otel.logs.enabled=true fails SessionFactory build for TABLE_PER_CLASS collections
* HHH-20783 hibernate.transactions{result=&quot;failure&quot;} metric can transiently go negative due to non-atomic counter reads, breaking the whole Prometheus scrape on Micrometer 1.14+
* HHH-20779 Envers: unwrap proxies in collection-change audit work units
* HHH-20776 CriteriaBuilder.literal() mistypes an enum constant declared with a class body
* HHH-20772 ARRAY_AGG column in Jakarta Data query method cannot be mapped to result type property
* HHH-20743 <code>hibernate-maven-plugin</code> <code>enhance</code> goal computes wrong class names when <code>fileSets</code> directory differs from <code>classesDirectory</code>
* HHH-20707 Missing import for inner interface type in CDI accessor metamodel methods
* HHH-20696 Implicit name of list index columns not applied by MetadataBuilder
* HHH-20661 HQL UNION fails when unioning java.util.Date from different attribute paths
* HHH-20624 StackOverflowError when creating entity manager with attribute converter hierarchy with generic parameter
* HHH-20515 Adjust default for SessionCheckMode on Session.findMultiple()
* HHH-20472 Generated metamodel class missing <code>List</code> import
* HHH-20452 <a href="https://github.com/OneToMany"><code>@​OneToMany</code></a> mapping silently dropped when orm.xml contributes a partial overlay (entity-listeners only) to an entity whose <a href="https://github.com/Id"><code>@​Id</code></a> is inherited from a <a href="https://github.com/MappedSuperclass"><code>@​MappedSuperclass</code></a>
* HHH-20438 Basic-array body predicates fail with AssertionError from SqmMappingModelHelper.resolveSqmPath
* HHH-20348 <code>DataException</code> / <code>ClassCastException</code> when aggregating primitive</p>
<p>** Task
* HHH-20736 Tune the content of javadocs to reduce the size of files published to Maven Central
* HHH-20710 Update to hibernate-models 1.1.2</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>43e2e9a</code></a> [Jenkins release job] Preparing release 7.4.6.Final</li>
<li><a href=""><code>cd34e60</code></a> [Jenkins release job] changelog.txt updated by release build 7.4.6.Final</li>
<li><a href=""><code>229571c</code></a> HHH-20710 Add test for generic Map subtype resolution with JSON mapping</li>
<li><a href=""><code>de419ce</code></a> HHH-20710 Update to hibernate-models 1.1.2</li>
<li><a href=""><code>284a4be</code></a> HHH-20788 Return null for TablePerSubclass and clarify informational nature o...</li>
<li><a href=""><code>f74ba58</code></a> Make testsuite fit for JDK 28 Valhalla preview</li>
<li><a href=""><code>33465fe</code></a> Add JDK 28 to the testing JDK list</li>
<li><a href=""><code>5e398fd</code></a> Skip some tests causing nightly failures on MySQL due to a bug</li>
<li><a href=""><code>cf53ffa</code></a> HHH-20783 Add a dedicated failed-transactions counter to Statistics</li>
<li><a href=""><code>f4e0be3</code></a> HHH-20772 add <a href="https://github.com/Incubating"><code>@​Incubating</code></a> to new Processor options</li>
<li>Additional commits viewable in <a href="https://github.com/hibernate/hibernate-orm/compare/7.4.5...7.4.6">compare view</a></li>
</ul>
</details>
<br />

Updates `org.hibernate.orm:hibernate-envers` from 7.4.5.Final to 7.4.6.Final
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/releases">org.hibernate.orm:hibernate-envers's releases</a>.</em></p>
<blockquote>
<h2>Release 7.4.6</h2>
<h1>Hibernate ORM 7.4.6.Final released</h1>
<p>Today, we published a new release of Hibernate ORM 7.4: 7.4.6.Final.</p>
<p>You can find the full list of 7.4.6.Final changes <a href="https://hibernate.atlassian.net/issues/?jql=project%20%3D%20HHH%20AND%20fixVersion%20%3D%207.4.6">here</a>.</p>
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
<p><em>Sourced from <a href="https://github.com/hibernate/hibernate-orm/blob/7.4.6/changelog.txt">org.hibernate.orm:hibernate-envers's changelog</a>.</em></p>
<blockquote>
<h2>Changes in 7.4.6.Final (August 23, 2026)</h2>
<p><a href="https://hibernate.atlassian.net/projects/HHH/versions/40133">https://hibernate.atlassian.net/projects/HHH/versions/40133</a></p>
<p>** Bug
* HHH-20788 [Quarkus 3.20.5 / Hibernate ORM 6.6.40.Final] quarkus.otel.logs.enabled=true fails SessionFactory build for TABLE_PER_CLASS collections
* HHH-20783 hibernate.transactions{result=&quot;failure&quot;} metric can transiently go negative due to non-atomic counter reads, breaking the whole Prometheus scrape on Micrometer 1.14+
* HHH-20779 Envers: unwrap proxies in collection-change audit work units
* HHH-20776 CriteriaBuilder.literal() mistypes an enum constant declared with a class body
* HHH-20772 ARRAY_AGG column in Jakarta Data query method cannot be mapped to result type property
* HHH-20743 <code>hibernate-maven-plugin</code> <code>enhance</code> goal computes wrong class names when <code>fileSets</code> directory differs from <code>classesDirectory</code>
* HHH-20707 Missing import for inner interface type in CDI accessor metamodel methods
* HHH-20696 Implicit name of list index columns not applied by MetadataBuilder
* HHH-20661 HQL UNION fails when unioning java.util.Date from different attribute paths
* HHH-20624 StackOverflowError when creating entity manager with attribute converter hierarchy with generic parameter
* HHH-20515 Adjust default for SessionCheckMode on Session.findMultiple()
* HHH-20472 Generated metamodel class missing <code>List</code> import
* HHH-20452 <a href="https://github.com/OneToMany"><code>@​OneToMany</code></a> mapping silently dropped when orm.xml contributes a partial overlay (entity-listeners only) to an entity whose <a href="https://github.com/Id"><code>@​Id</code></a> is inherited from a <a href="https://github.com/MappedSuperclass"><code>@​MappedSuperclass</code></a>
* HHH-20438 Basic-array body predicates fail with AssertionError from SqmMappingModelHelper.resolveSqmPath
* HHH-20348 <code>DataException</code> / <code>ClassCastException</code> when aggregating primitive</p>
<p>** Task
* HHH-20736 Tune the content of javadocs to reduce the size of files published to Maven Central
* HHH-20710 Update to hibernate-models 1.1.2</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>43e2e9a</code></a> [Jenkins release job] Preparing release 7.4.6.Final</li>
<li><a href=""><code>cd34e60</code></a> [Jenkins release job] changelog.txt updated by release build 7.4.6.Final</li>
<li><a href=""><code>229571c</code></a> HHH-20710 Add test for generic Map subtype resolution with JSON mapping</li>
<li><a href=""><code>de419ce</code></a> HHH-20710 Update to hibernate-models 1.1.2</li>
<li><a href=""><code>284a4be</code></a> HHH-20788 Return null for TablePerSubclass and clarify informational nature o...</li>
<li><a href=""><code>f74ba58</code></a> Make testsuite fit for JDK 28 Valhalla preview</li>
<li><a href=""><code>33465fe</code></a> Add JDK 28 to the testing JDK list</li>
<li><a href=""><code>5e398fd</code></a> Skip some tests causing nightly failures on MySQL due to a bug</li>
<li><a href=""><code>cf53ffa</code></a> HHH-20783 Add a dedicated failed-transactions counter to Statistics</li>
<li><a href=""><code>f4e0be3</code></a> HHH-20772 add <a href="https://github.com/Incubating"><code>@​Incubating</code></a> to new Processor options</li>
<li>Additional commits viewable in <a href="https://github.com/hibernate/hibernate-orm/compare/7.4.5...7.4.6">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7ec569f4849c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.