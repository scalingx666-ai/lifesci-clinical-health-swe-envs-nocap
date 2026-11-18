# Issue

**Title:** github-actions(deps): bump docker/login-action from 4.5.1 to 4.5.2

## Description

Bumps [docker/login-action](https://github.com/docker/login-action) from 4.5.1 to 4.5.2.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/docker/login-action/releases">docker/login-action's releases</a>.</em></p>
<blockquote>
<h2>v4.5.2</h2>
<ul>
<li>Surface Docker Hub OIDC error responses by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/login-action#1058</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/login-action/compare/v4.5.1...v4.5.2">https://github.com/docker/login-action/compare/v4.5.1...v4.5.2</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>371161b</code></a> Merge pull request <a href="">#1058</a> from crazy-max/fix-dockerhub-oidc-error-handling</li>
<li><a href=""><code>5dc73df</code></a> chore: update generated content</li>
<li><a href=""><code>2aa1ede</code></a> surface Docker Hub OIDC error responses</li>
<li>See full diff in <a href="https://github.com/docker/login-action/compare/abd2ef45e78c5afb21d64d4ca52ee8550d9572c7...371161bbe7024a29a25c5e19bfcbc0804fe9ad2c">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=docker/login-action&package-manager=github_actions&previous-version=4.5.1&new-version=4.5.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `58c1d9f3506e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.