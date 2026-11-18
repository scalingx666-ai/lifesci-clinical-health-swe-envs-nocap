# Issue

**Title:** maven(deps): bump org.codehaus.mojo:build-helper-maven-plugin from 3.6.1 to 3.6.2

## Description

Bumps [org.codehaus.mojo:build-helper-maven-plugin](https://github.com/mojohaus/build-helper-maven-plugin) from 3.6.1 to 3.6.2.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/mojohaus/build-helper-maven-plugin/releases">org.codehaus.mojo:build-helper-maven-plugin's releases</a>.</em></p>
<blockquote>
<h2>3.6.2</h2>
<!-- raw HTML omitted -->
<h2>🐛 Bug Fixes</h2>
<ul>
<li>Replace raw <code>NPEx</code> with customized exception message (<a href="">#239</a>) <a href="https://github.com/pzygielo"><code>@​pzygielo</code></a></li>
</ul>
<h2>👻 Maintenance</h2>
<ul>
<li>Remove redundant maven-resolver-api dependency and ignore Resolver/SLF4J 2.x in Dependabot (<a href="">#248</a>) <a href="https://github.com/slachiewicz"><code>@​slachiewicz</code></a></li>
</ul>
<h2>📦 Dependency updates</h2>
<!-- raw HTML omitted -->
<ul>
<li>Remove redundant maven-resolver-api dependency and ignore Resolver/SLF4J 2.x in Dependabot (<a href="">#248</a>) <a href="https://github.com/slachiewicz"><code>@​slachiewicz</code></a></li>
<li>Bump org.codehaus.plexus:plexus-utils from 4.0.3 to 4.1.0 (<a href="">#247</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump apache/maven-gh-actions-shared/.github/workflows/release-drafter.yml from 4 to 5 (<a href="">#244</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump org.codehaus.mojo:mojo-parent from 96 to 97 (<a href="">#246</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump apache/maven-gh-actions-shared/.github/workflows/maven-verify.yml from 4 to 5 (<a href="">#245</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump org.codehaus.plexus:plexus-utils from 4.0.2 to 4.0.3 (<a href="">#241</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump org.codehaus.mojo:mojo-parent from 95 to 96 (<a href="">#240</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump org.codehaus.mojo:mojo-parent from 94 to 95 (<a href="">#235</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump org.codehaus.mojo:mojo-parent from 93 to 94 (<a href="">#233</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump org.codehaus.mojo:mojo-parent from 92 to 93 (<a href="">#232</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
<li>Bump org.codehaus.mojo:mojo-parent from 91 to 92 (<a href="">#231</a>) @<a href="https://github.com/apps/dependabot">dependabot[bot]</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>813bc7d</code></a> [maven-release-plugin] prepare release 3.6.2</li>
<li><a href=""><code>07d9109</code></a> Remove redundant maven-resolver-api and ignore Resolver/SLF4J 2.x in Dependabot</li>
<li><a href=""><code>9abd552</code></a> Bump org.codehaus.plexus:plexus-utils from 4.0.3 to 4.1.0</li>
<li><a href=""><code>3c15526</code></a> Bump apache/maven-gh-actions-shared/.github/workflows/release-drafter.yml</li>
<li><a href=""><code>3b1f104</code></a> Bump org.codehaus.mojo:mojo-parent from 96 to 97</li>
<li><a href=""><code>1749855</code></a> Bump apache/maven-gh-actions-shared/.github/workflows/maven-verify.yml</li>
<li><a href=""><code>5230041</code></a> Bump org.codehaus.plexus:plexus-utils from 4.0.2 to 4.0.3</li>
<li><a href=""><code>c0e9375</code></a> Delete .github/release-drafter.yml</li>
<li><a href=""><code>84a839e</code></a> Bump org.codehaus.mojo:mojo-parent from 95 to 96</li>
<li><a href=""><code>a85c668</code></a> Replace raw <code>NPEx</code> with customized exception message</li>
<li>Additional commits viewable in <a href="https://github.com/mojohaus/build-helper-maven-plugin/compare/3.6.1...3.6.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.codehaus.mojo:build-helper-maven-plugin&package-manager=maven&previous-version=3.6.1&new-version=3.6.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `52f53c9595bc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.