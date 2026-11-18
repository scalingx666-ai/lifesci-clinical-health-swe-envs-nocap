# Issue

**Title:** github-actions(deps): bump github/codeql-action from 4.37.4 to 4.37.5

## Description

Bumps [github/codeql-action](https://github.com/github/codeql-action) from 4.37.4 to 4.37.5.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/github/codeql-action/releases">github/codeql-action's releases</a>.</em></p>
<blockquote>
<h2>v4.37.5</h2>
<ul>
<li>Fixed a bug where a network error while streaming the download of the CodeQL bundle could terminate the <code>init</code> Action instead of falling back to downloading the bundle before extracting it. <a href="">#4061</a></li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/github/codeql-action/blob/main/CHANGELOG.md">github/codeql-action's changelog</a>.</em></p>
<blockquote>
<h2>4.37.5 - 03 Aug 2026</h2>
<ul>
<li>Fixed a bug where a network error while streaming the download of the CodeQL bundle could terminate the <code>init</code> Action instead of falling back to downloading the bundle before extracting it. <a href="">#4061</a></li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>d1ba80a</code></a> Merge pull request <a href="">#4067</a> from github/update-v4.37.5-1cd4d01d5</li>
<li><a href=""><code>e74600b</code></a> Update changelog for v4.37.5</li>
<li><a href=""><code>1cd4d01</code></a> Merge pull request <a href="">#4061</a> from github/henrymercer/turbo-system</li>
<li><a href=""><code>d2bfc30</code></a> Merge pull request <a href="">#4050</a> from github/mbg/status/registries</li>
<li><a href=""><code>68028fc</code></a> Merge pull request <a href="">#4062</a> from github/sam-robson/migrate-enterprise-release-pat</li>
<li><a href=""><code>c29563e</code></a> ci: use federated enterprise release PAT</li>
<li><a href=""><code>155e522</code></a> Link the PR from the changelog entry</li>
<li><a href=""><code>2d3b351</code></a> Handle network errors when streaming the CodeQL bundle download</li>
<li><a href=""><code>5d3eb98</code></a> Merge pull request <a href="">#4055</a> from github/dependabot/npm_and_yarn/npm-minor-203262...</li>
<li><a href=""><code>c5f739b</code></a> Merge branch 'main' into dependabot/npm_and_yarn/npm-minor-2032624187</li>
<li>Additional commits viewable in <a href="https://github.com/github/codeql-action/compare/v4.37.4...v4.37.5">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=github/codeql-action&package-manager=github_actions&previous-version=4.37.4&new-version=4.37.5)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `50b999032295`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.