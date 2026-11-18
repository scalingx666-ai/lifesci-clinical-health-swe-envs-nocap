# Issue

**Title:** chore: bump virtualenv from 21.7.12 to 21.7.13 in /backend

## Description

Bumps [virtualenv](https://github.com/pypa/virtualenv) from 21.7.12 to 21.7.13.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pypa/virtualenv/releases">virtualenv's releases</a>.</em></p>
<blockquote>
<h2>21.7.13</h2>
<!-- raw HTML omitted -->
<h2>What's Changed</h2>
<ul>
<li>👷 ci: correct a stale checkout pin comment by <a href="https://github.com/gaborbernat"><code>@​gaborbernat</code></a> in <a href="">pypa/virtualenv#3254</a></li>
<li>🔧 chore: drop misc as a changelog fragment type by <a href="https://github.com/gaborbernat"><code>@​gaborbernat</code></a> in <a href="">pypa/virtualenv#3255</a></li>
<li>👷 ci: scope the nushell apt key to its own repo by <a href="https://github.com/gaborbernat"><code>@​gaborbernat</code></a> in <a href="">pypa/virtualenv#3253</a></li>
<li>🐛 fix(activation): stop path command injection in bash and fish by <a href="https://github.com/gaborbernat"><code>@​gaborbernat</code></a> in <a href="">pypa/virtualenv#3252</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/pypa/virtualenv/compare/21.7.12...21.7.13">https://github.com/pypa/virtualenv/compare/21.7.12...21.7.13</a></p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/pypa/virtualenv/blob/main/docs/changelog.rst">virtualenv's changelog</a>.</em></p>
<blockquote>
<h1>Bugfixes - 21.7.13</h1>
<ul>
<li>Fix <code>activate</code> and <code>activate.fish</code> running commands embedded in the virtual environment path or in the
interpreter's Tcl/Tk library paths. (:issue:<code>3252</code>)</li>
</ul>
<hr />
<p>v21.7.12 (2026-09-18)</p>
<hr />
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>0c295ff</code></a> release 21.7.13</li>
<li><a href=""><code>4d5a105</code></a> 🐛 fix(activation): stop path command injection in bash and fish (<a href="">#3252</a>)</li>
<li><a href=""><code>0525dce</code></a> 👷 ci: scope the nushell apt key to its own repo (<a href="">#3253</a>)</li>
<li><a href=""><code>aa8323a</code></a> 🔧 chore: drop misc as a changelog fragment type (<a href="">#3255</a>)</li>
<li><a href=""><code>a435477</code></a> 👷 ci: correct a stale checkout pin comment (<a href="">#3254</a>)</li>
<li>See full diff in <a href="https://github.com/pypa/virtualenv/compare/21.7.12...21.7.13">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=virtualenv&package-manager=uv&previous-version=21.7.12&new-version=21.7.13)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
You can disable automated security fix PRs for this repo from the [Security Alerts page](https://github.com/the-momentum/open-wearables/network/alerts).

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fa3c95a07f95`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.