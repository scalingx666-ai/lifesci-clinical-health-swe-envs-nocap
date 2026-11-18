# Issue

**Title:** github-actions(deps): bump actions/setup-java from 6.0.0 to 6.1.0

## Description

Bumps [actions/setup-java](https://github.com/actions/setup-java) from 6.0.0 to 6.1.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/setup-java/releases">actions/setup-java's releases</a>.</em></p>
<blockquote>
<h2>v6.1.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Preserve compound Liberica build versions from .sdkmanrc by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> with <a href="https://github.com/Copilot"><code>@​Copilot</code></a> in <a href="">actions/setup-java#1268</a></li>
<li>Support Temurin on Linux RISC-V by <a href="https://github.com/yawkat"><code>@​yawkat</code></a> in <a href="">actions/setup-java#1269</a></li>
<li>Stop GPG agent before removing signature-verification home by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> with <a href="https://github.com/Copilot"><code>@​Copilot</code></a> in <a href="">actions/setup-java#1273</a></li>
<li>Prefer Zulu 4-segment hotfix builds when resolving version ranges by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1278</a></li>
<li>Support Temurin JEP 322 patch versions like 26.0.2.1+1 by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1279</a></li>
<li>chore(deps): bump undici from 6.28.0 to 6.29.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/setup-java#1274</a></li>
<li>chore(deps): bump the monthly-npm-updates group with 13 updates by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/setup-java#1276</a></li>
<li>feat: support Maven server credential origins by <a href="https://github.com/YunaBraska"><code>@​YunaBraska</code></a> in <a href="">actions/setup-java#1282</a></li>
<li>Support Maven plugin repositories in generated settings.xml by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1286</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/yawkat"><code>@​yawkat</code></a> made their first contribution in <a href="">actions/setup-java#1269</a></li>
<li><a href="https://github.com/YunaBraska"><code>@​YunaBraska</code></a> made their first contribution in <a href="">actions/setup-java#1282</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/setup-java/compare/v6.0.1...v6.1.0">https://github.com/actions/setup-java/compare/v6.0.1...v6.1.0</a></p>
<h2>v6.0.1</h2>
<h2>What's Changed</h2>
<ul>
<li>Fix failing GitHub Actions job for temurin 17 by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> with <a href="https://github.com/Copilot"><code>@​Copilot</code></a> in <a href="">actions/setup-java#1259</a></li>
<li>Fix Temurin EA E2E signature verification by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> with <a href="https://github.com/Copilot"><code>@​Copilot</code></a> in <a href="">actions/setup-java#1260</a></li>
<li>Fix Alpine GPG verification failures and support multiple keys by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1262</a></li>
<li>Fix import-safe checks when scripts are run from a path with symlinks by <a href="https://github.com/otaconix"><code>@​otaconix</code></a> in <a href="">actions/setup-java#1265</a></li>
<li>Avoid macOS GPG socket overflow on long runner paths by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> with <a href="https://github.com/Copilot"><code>@​Copilot</code></a> in <a href="">actions/setup-java#1266</a></li>
<li>Complete v6 release highlights in README by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1254</a></li>
<li>Group and slow routine Dependabot updates by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1255</a></li>
<li>chore(deps-dev): update eslint and globals by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/setup-java#1256</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/otaconix"><code>@​otaconix</code></a> made their first contribution in <a href="">actions/setup-java#1265</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/setup-java/compare/v6.0.0...v6.0.1">https://github.com/actions/setup-java/compare/v6.0.0...v6.0.1</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li>See full diff in <a href="https://github.com/actions/setup-java/compare/v6...v6.1.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/setup-java&package-manager=github_actions&previous-version=6.0.0&new-version=6.1.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `29a868a6403e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.