# Issue

**Title:** Bump eslint-utils from 1.4.0 to 1.4.3 in /webcore

## Description

Bumps [eslint-utils](https://github.com/mysticatea/eslint-utils) from 1.4.0 to 1.4.3.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/mysticatea/eslint-utils/releases">eslint-utils's releases</a>.</em></p>
<blockquote>
<h2>v1.4.3</h2>
<h2>🐛 Bug fixes</h2>
<ul>
<li>8f9e481ecc1204c7a1331b697f97903f90c75154 fixed false positive of <code>ReferenceTracker</code>.</li>
</ul>
<h2>v1.4.2</h2>
<h2>🐛 Bug fixes</h2>
<ul>
<li>e4cb01498df6096b66edb0c78965ee6f47d3ac77 fixed a regression of the previous release.</li>
</ul>
<h2>v1.4.1</h2>
<h2>🐛 Bug fixes</h2>
<ul>
<li>c119e832952c8c653bd4f21e39eb9f7ce48e5947 fixed <code>getStaticValue()</code> function to handle <code>null</code> literal correctly even if runtimes don't support BigInt natively.</li>
<li>587cca2f82c245f5fc4a8b9fb2cf6b35c0d02552 fixed <code>getStringIfConstant()</code> function to handle regular expression literals and BigInt literals even if runtimes don't support those.</li>
<li>08158db1c98fd71cf0f32ddefbc147e2620e724c fixed GHSA-3gx7-xhv7-5mx3.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>23f4ddc</code></a> 🔖 1.4.3</li>
<li><a href=""><code>8f9e481</code></a> 🐛 fix reference tracker false positive</li>
<li><a href=""><code>6633278</code></a> ⚒ fix test scripts</li>
<li><a href=""><code>7c8e67c</code></a> ⚒ fix build scripts</li>
<li><a href=""><code>41ff95e</code></a> ⚒ update dependencies</li>
<li><a href=""><code>4942012</code></a> ⚒ fix build scripts</li>
<li><a href=""><code>f1c8d02</code></a> ⚒ update build scripts</li>
<li><a href=""><code>a88598a</code></a> Create FUNDING.yml</li>
<li><a href=""><code>4e1bc07</code></a> 1.4.2</li>
<li><a href=""><code>e4cb014</code></a> 🐛 add null test</li>
<li>Additional commits viewable in <a href="https://github.com/mysticatea/eslint-utils/compare/v1.4.0...v1.4.3">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=eslint-utils&package-manager=npm_and_yarn&previous-version=1.4.0&new-version=1.4.3)](https://help.github.com/articles/configuring-automated-security-fixes)

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
- `@dependabot merge` will merge this PR after your CI passes on it
- `@dependabot squash and merge` will squash and merge this PR after your CI passes on it
- `@dependabot cancel merge` will cancel a previously requested merge and block automerging
- `@dependabot reopen` will reopen this PR if it is closed
- `@dependabot close` will close this PR and stop Dependabot recreating it. You can achieve the same result by closing it manually
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)
- `@dependabot use these labels` will set the current labels as the default for future PRs for this repo and language
- `@dependabot use these reviewers` will set the current reviewers as the default for future PRs for this repo and language
- `@dependabot use these assignees` will set the current assignees as the default for future PRs for this repo and language
- `@dependabot use this milestone` will set the current milestone as the default for future PRs for this repo and language

You can disable automated security fix PRs for this repo from the [Security Alerts page](https://github.com/bioinformatics-ua/dicoogle/network/alerts).

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ce672e3b1026`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.