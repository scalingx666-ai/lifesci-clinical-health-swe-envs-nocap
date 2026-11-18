# Issue

**Title:** chore: bump authlib from 1.8.0 to 1.9.1 in /mcp

## Description

Bumps [authlib](https://github.com/authlib/authlib) from 1.8.0 to 1.9.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/authlib/authlib/releases">authlib's releases</a>.</em></p>
<blockquote>
<h2>v1.9.1</h2>
<p>Changelog: <a href="https://docs.authlib.org/en/stable/upgrades/changelog.html#changelog-1-9-1">https://docs.authlib.org/en/stable/upgrades/changelog.html#changelog-1-9-1</a></p>
<h2>What's Changed</h2>
<ul>
<li>Use scriv to handle the changelog by <a href="https://github.com/azmeuk"><code>@​azmeuk</code></a> in <a href="">authlib/authlib#954</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/authlib/authlib/compare/v1.9.0...v1.9.1">https://github.com/authlib/authlib/compare/v1.9.0...v1.9.1</a></p>
<h2>v1.9.0</h2>
<h2>What's Changed</h2>
<ul>
<li>feat: add Identity Assertion JWT Authorization Grant (ID-JAG) by <a href="https://github.com/BinoyOza-okta"><code>@​BinoyOza-okta</code></a> in <a href="">authlib/authlib#898</a></li>
<li>Fix empty signatures validation in JWS JSON deserialization by <a href="https://github.com/loporto"><code>@​loporto</code></a> in <a href="">authlib/authlib#938</a></li>
<li>fix(jose): reject boolean values for NumericDate claims by <a href="https://github.com/cpruijsen"><code>@​cpruijsen</code></a> in <a href="">authlib/authlib#942</a></li>
<li>fix(client): avoid duplicated OAuth 1.0 parameters in signed requests by <a href="https://github.com/cpruijsen"><code>@​cpruijsen</code></a> in <a href="">authlib/authlib#943</a></li>
<li>OAuth2 token fetch crashes with JSONDecodeError instead of a catchable error on rate-limit responses by <a href="https://github.com/juneja-varun"><code>@​juneja-varun</code></a> in <a href="">authlib/authlib#929</a></li>
<li>docs: add i18n wrappers in conf.py and templates by <a href="https://github.com/hwhsu1231"><code>@​hwhsu1231</code></a> in <a href="">authlib/authlib#901</a></li>
<li>fix(oauth): enforce JOSE key, scope, and audience validation by <a href="https://github.com/lepture"><code>@​lepture</code></a> in <a href="">authlib/authlib#945</a></li>
<li>AsyncOpenIDMixin.parse_id_token: return None when id_token is absent, matching the sync client by <a href="https://github.com/ckarnell"><code>@​ckarnell</code></a> in <a href="">authlib/authlib#924</a></li>
<li>fix(oauth): enforce nonce and JAR request validation by <a href="https://github.com/lepture"><code>@​lepture</code></a> in <a href="">authlib/authlib#949</a></li>
<li>fix(oauth): require client authentication for ID-JAG grants by <a href="https://github.com/lepture"><code>@​lepture</code></a> in <a href="">authlib/authlib#955</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/BinoyOza-okta"><code>@​BinoyOza-okta</code></a> made their first contribution in <a href="">authlib/authlib#898</a></li>
<li><a href="https://github.com/loporto"><code>@​loporto</code></a> made their first contribution in <a href="">authlib/authlib#938</a></li>
<li><a href="https://github.com/cpruijsen"><code>@​cpruijsen</code></a> made their first contribution in <a href="">authlib/authlib#942</a></li>
<li><a href="https://github.com/juneja-varun"><code>@​juneja-varun</code></a> made their first contribution in <a href="">authlib/authlib#929</a></li>
<li><a href="https://github.com/hwhsu1231"><code>@​hwhsu1231</code></a> made their first contribution in <a href="">authlib/authlib#901</a></li>
<li><a href="https://github.com/ckarnell"><code>@​ckarnell</code></a> made their first contribution in <a href="">authlib/authlib#924</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/authlib/authlib/compare/v1.8.0...v1.9.0">https://github.com/authlib/authlib/compare/v1.8.0...v1.9.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>46b9487</code></a> chore: release 1.9.1</li>
<li><a href=""><code>abb3f49</code></a> docs: use the issuer identifier as ID-JAG audience and fix broken links</li>
<li><a href=""><code>1bd2a31</code></a> Merge commit from fork</li>
<li><a href=""><code>311da11</code></a> docs: more detailed PKCE instructions</li>
<li><a href=""><code>873f72c</code></a> docs: rpinitiated instructions</li>
<li><a href=""><code>4ff30db</code></a> Merge commit from fork</li>
<li><a href=""><code>9a86ff3</code></a> docs: rpinitiated sequence chart</li>
<li><a href=""><code>1c35757</code></a> docs: RFC 9101 sequence chart</li>
<li><a href=""><code>a755e28</code></a> docs: add a sequence diagram to the token introspection page</li>
<li><a href=""><code>1996c56</code></a> docs: PKCE flow chart illustration</li>
<li>Additional commits viewable in <a href="https://github.com/authlib/authlib/compare/v1.8.0...v1.9.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=authlib&package-manager=uv&previous-version=1.8.0&new-version=1.9.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `95f14344ea23`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.