# Issue

**Title:** github-actions(deps): bump docker/setup-qemu-action from 4.3.0 to 4.4.0

## Description

Bumps [docker/setup-qemu-action](https://github.com/docker/setup-qemu-action) from 4.3.0 to 4.4.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/docker/setup-qemu-action/releases">docker/setup-qemu-action's releases</a>.</em></p>
<blockquote>
<h2>v4.4.0</h2>
<ul>
<li>Use the shared error helper for Docker commands by <a href="https://github.com/crazy-max"><code>@​crazy-max</code></a> in <a href="">docker/setup-qemu-action#345</a></li>
<li>Bump <code>@​docker/actions-toolkit</code> from 0.96.0 to 0.100.0 in <a href="">docker/setup-qemu-action#344</a></li>
<li>Bump <code>@​humanfs/node</code> from 0.16.7 to 0.16.8 in <a href="">docker/setup-qemu-action#340</a></li>
<li>Bump js-yaml from 4.3.1 to 4.3.2 in <a href="">docker/setup-qemu-action#342</a></li>
<li>Bump postcss-selector-parser from 7.1.1 to 7.1.5 in <a href="">docker/setup-qemu-action#337</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/docker/setup-qemu-action/compare/v4.3.0...v4.4.0">https://github.com/docker/setup-qemu-action/compare/v4.3.0...v4.4.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>9901266</code></a> Merge pull request <a href="">#342</a> from docker/dependabot/npm_and_yarn/js-yaml-4.3.2</li>
<li><a href=""><code>9364d8b</code></a> Merge pull request <a href="">#340</a> from docker/dependabot/npm_and_yarn/humanfs/node-0.16.8</li>
<li><a href=""><code>95c3240</code></a> Merge pull request <a href="">#337</a> from docker/dependabot/npm_and_yarn/postcss-selector-...</li>
<li><a href=""><code>c24671a</code></a> Merge pull request <a href="">#338</a> from docker/dependabot/github_actions/codeql-actions-...</li>
<li><a href=""><code>fa83965</code></a> Merge pull request <a href="">#345</a> from crazy-max/shared-error-helpers</li>
<li><a href=""><code>f396a65</code></a> build(deps): bump the codeql-actions group across 1 directory with 2 updates</li>
<li><a href=""><code>a63df2f</code></a> chore: update generated content</li>
<li><a href=""><code>3e4165f</code></a> use the shared error helper for Docker commands</li>
<li><a href=""><code>18c52d9</code></a> Merge pull request <a href="">#344</a> from docker/dependabot/npm_and_yarn/docker/actions-to...</li>
<li><a href=""><code>896cbed</code></a> [dependabot skip] chore: update generated content</li>
<li>Additional commits viewable in <a href="https://github.com/docker/setup-qemu-action/compare/1f40c72289eff860ee54a304f1438e3cff362e0a...99012661954931238ded8c8b007157a8430204e1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=docker/setup-qemu-action&package-manager=github_actions&previous-version=4.3.0&new-version=4.4.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `51c5652b5fe8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.