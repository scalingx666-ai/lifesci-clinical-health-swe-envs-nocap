# Issue

**Title:** maven(deps): bump com.google.guava:guava from 33.7.1-jre to 33.7.2-jre

## Description

Bumps [com.google.guava:guava](https://github.com/google/guava) from 33.7.1-jre to 33.7.2-jre.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/google/guava/releases">com.google.guava:guava's releases</a>.</em></p>
<blockquote>
<h2>33.7.2</h2>
<h3>Maven</h3>
<pre lang="xml"><code>&lt;dependency&gt;
  &lt;groupId&gt;com.google.guava&lt;/groupId&gt;
  &lt;artifactId&gt;guava&lt;/artifactId&gt;
  &lt;version&gt;33.7.2-jre&lt;/version&gt;
  &lt;!-- or, for Android: --&gt;
  &lt;version&gt;33.7.2-android&lt;/version&gt;
&lt;/dependency&gt;
</code></pre>
<h3>Jar files</h3>
<ul>
<li><a href="https://repo1.maven.org/maven2/com/google/guava/guava/33.7.2-jre/guava-33.7.2-jre.jar">33.7.2-jre.jar</a></li>
<li><a href="https://repo1.maven.org/maven2/com/google/guava/guava/33.7.2-android/guava-33.7.2-android.jar">33.7.2-android.jar</a></li>
</ul>
<p>Guava requires
<a href="https://github.com/google/guava/wiki/UseGuavaInYourBuild#what-about-guavas-own-dependencies">one runtime dependency</a>,
which you can download here:</p>
<ul>
<li><a href="https://repo1.maven.org/maven2/com/google/guava/failureaccess/1.0.3/failureaccess-1.0.3.jar">failureaccess-1.0.3.jar</a></li>
</ul>
<h3>Javadoc</h3>
<ul>
<li><a href="https://guava.dev/releases/33.7.2-jre/api/docs/">33.7.2-jre</a></li>
<li><a href="https://guava.dev/releases/33.7.2-android/api/docs/">33.7.2-android</a></li>
</ul>
<h3>JDiff</h3>
<ul>
<li><a href="https://guava.dev/releases/33.7.2-jre/api/diffs/">33.7.2-jre vs. 33.7.1-jre</a></li>
<li><a href="https://guava.dev/releases/33.7.2-android/api/diffs/">33.7.2-android vs. 33.7.1-android</a></li>
<li><a href="https://guava.dev/releases/33.7.2-android/api/androiddiffs/">33.7.2-android vs. 33.7.2-jre</a></li>
</ul>
<h3>Changelog</h3>
<ul>
<li><code>collect</code>: Changed <code>MapMaker</code>, <code>CompactHashMap</code>, and <code>CompactHashSet</code> deserialization to <a href="https://github.com/google/guava/security/advisories/GHSA-xxph-c9ww-hj94">avoid eagerly allocating as much memory as a serialization payload requests</a>. (a0d0c36432)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li>See full diff in <a href="https://github.com/google/guava/commits">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=com.google.guava:guava&package-manager=maven&previous-version=33.7.1-jre&new-version=33.7.2-jre)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `015b9c67043f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.