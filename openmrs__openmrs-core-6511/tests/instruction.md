# Issue

**Title:** maven(deps): bump org.dbunit:dbunit from 3.5.0 to 3.5.1

## Description

Bumps [org.dbunit:dbunit](https://github.com/dbunit/dbunit-extension) from 3.5.0 to 3.5.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/dbunit/dbunit-extension/releases">org.dbunit:dbunit's releases</a>.</em></p>
<blockquote>
<h2>3.5.1</h2>
<h3>Fixed Bugs</h3>
<ul>
<li>Fix a 3.5.0 regression (introduced by issue <a href="">dbunit/dbunit-extension#496</a> fix) where FlatXmlProducer added every table from an explicitly-supplied metadata IDataSet as an empty table, not just tables actually present in the flat XML body: FlatXmlDataSetBuilder#setMetaDataSet(IDataSet) is documented as supplying column metadata only, but a broad metadata source such as a live database's full IDataSet (e.g. via DatabaseConnection#createDataSet()) was being read as if it enumerated the fixture's own tables, so DELETE_ALL/CLEAN_INSERT ended up touching every table in that broader source instead of only the ones the XML body mentions. FlatXmlProducer's issue <a href="">dbunit/dbunit-extension#496</a> empty-table backfill now only runs when the metadata source is DTD-derived (a FlatDtdDataSet, whether parsed inline from the flat XML's own DOCTYPE or supplied via FlatXmlDataSetBuilder#setMetaDataSetFromDtd), restoring pre-3.5.0 behavior for any other explicitly-supplied metadata dataset. Issue: 951. Thanks to tkrah.</li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/dbunit/dbunit-extension/compare/dbunit-3.5.0...dbunit-3.5.1">https://github.com/dbunit/dbunit-extension/compare/dbunit-3.5.0...dbunit-3.5.1</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>a1f5944</code></a> docs(site): Update index.adoc with 3.5.1 release</li>
<li><a href=""><code>2c76618</code></a> chore(release): Prep 3.5.1</li>
<li><a href=""><code>4674c5d</code></a> fix(dataset): Restrict FlatXmlProducer empty-table backfill to DTD metadata</li>
<li><a href=""><code>085c74d</code></a> docs: Convert lists and words to page links</li>
<li><a href=""><code>32a8e00</code></a> [maven-release-plugin] prepare for next development iteration</li>
<li>See full diff in <a href="https://github.com/dbunit/dbunit-extension/compare/dbunit-3.5.0...dbunit-3.5.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.dbunit:dbunit&package-manager=maven&previous-version=3.5.0&new-version=3.5.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4793794c23e4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.