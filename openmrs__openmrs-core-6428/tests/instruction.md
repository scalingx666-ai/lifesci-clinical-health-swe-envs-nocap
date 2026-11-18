# Issue

**Title:** github-actions(deps): bump actions/setup-java from 5.6.0 to 5.7.0

## Description

Bumps [actions/setup-java](https://github.com/actions/setup-java) from 5.6.0 to 5.7.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/setup-java/releases">actions/setup-java's releases</a>.</em></p>
<blockquote>
<h2>v5.7.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Fix npm audit failures on releases/v5 by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1154</a></li>
<li>Backport <a href="">#1151</a>: Fix missing wrapper cache distributions by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1153</a></li>
<li>Deprecate legacy Adopt distributions in v5 by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1186</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/setup-java/compare/v5.6.0...v5.7.0">https://github.com/actions/setup-java/compare/v5.6.0...v5.7.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>b6effb0</code></a> Deprecate legacy Adopt distributions in v5 (<a href="">#1186</a>)</li>
<li><a href=""><code>e498d2a</code></a> Backport <a href="">#1151</a>: Fix missing wrapper cache distributions (<a href="">#1153</a>)</li>
<li><a href=""><code>6a3384d</code></a> Fix npm audit failures on releases/v5 (<a href="">#1154</a>)</li>
<li>See full diff in <a href="https://github.com/actions/setup-java/compare/v5.6.0...v5.7.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/setup-java&package-manager=github_actions&previous-version=5.6.0&new-version=5.7.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e3331f69a987`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.