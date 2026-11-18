# Issue

**Title:** maven(deps): bump org.springframework.security:spring-security-bom from 7.0.7 to 7.1.1

## Description

Bumps [org.springframework.security:spring-security-bom](https://github.com/spring-projects/spring-security) from 7.0.7 to 7.1.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/spring-projects/spring-security/releases">org.springframework.security:spring-security-bom's releases</a>.</em></p>
<blockquote>
<h2>7.1.1</h2>
<h2>:star: New Features</h2>
<ul>
<li>Fix Broken <code>DefaultLoginPageGeneratingFilter</code> Javadoc Link <a href="">#19252</a></li>
<li>Remove BeanResolver Null Checks <a href="">#19209</a></li>
<li>Remove Unnecessary <code>AuthorizationDecision</code> Cast <a href="">#19283</a></li>
<li>Update One-Time Token Docs for Renamed APIs <a href="">#19274</a></li>
</ul>
<h2>:beetle: Bug Fixes</h2>
<ul>
<li>Correct validation logic in CasAuthenticationToken <a href="">#19372</a></li>
<li>Differentiate Forwarded and X-Forwarded headers in proxy docs <a href="">#19477</a></li>
<li>Find mixed-case names in InMemoryUserDetailsManager#changePassword <a href="">#19539</a></li>
<li>Fix <code>OAuth2PushedAuthorizationRequestUri</code> parsing <a href="">#19445</a></li>
<li>Update JavaDoc Links in Reference <a href="">#19199</a></li>
<li>Validate Parameter in setPostAuthenticationChecks <a href="">#19277</a></li>
</ul>
<h2>:hammer: Dependency Upgrades</h2>
<ul>
<li>Bump <code>@springio</code>/antora-extensions from 1.14.12 to 1.14.13 in /docs <a href="">#19503</a></li>
<li>Bump actions/checkout from 6.0.3 to 7.0.0 <a href="">#19351</a></li>
<li>Bump actions/checkout from 7.0.0 to 7.0.1 <a href="">#19464</a></li>
<li>Bump actions/setup-java from 5.2.0 to 5.3.0 <a href="">#19352</a></li>
<li>Bump actions/setup-java from 5.3.0 to 5.4.0 <a href="">#19380</a></li>
<li>Bump actions/setup-java from 5.4.0 to 5.5.0 <a href="">#19430</a></li>
<li>Bump actions/setup-java from 5.5.0 to 5.6.0 <a href="">#19453</a></li>
<li>Bump actions/setup-java from 5.6.0 to 5.7.0 <a href="">#19501</a></li>
<li>Bump antora from 3.2.0-alpha.12 to 3.2.0-rc.2 in /docs <a href="">#19385</a></li>
<li>Bump ch.qos.logback:logback-classic from 1.5.34 to 1.5.35 <a href="">#19374</a></li>
<li>Bump ch.qos.logback:logback-classic from 1.5.35 to 1.5.36 <a href="">#19389</a></li>
<li>Bump ch.qos.logback:logback-classic from 1.5.36 to 1.5.37 <a href="">#19396</a></li>
<li>Bump ch.qos.logback:logback-classic from 1.5.37 to 1.5.38 <a href="">#19431</a></li>
<li>Bump ch.qos.logback:logback-classic from 1.5.38 to 1.6.0 <a href="">#19467</a></li>
<li>Bump ch.qos.logback:logback-classic from 1.6.0 to 1.6.1 <a href="">#19476</a></li>
<li>Bump ch.qos.logback:logback-classic from 1.6.1 to 1.6.2 <a href="">#19556</a></li>
<li>Bump ch.qos.logback:logback-classic from 1.6.2 to 1.6.3 <a href="">#19564</a></li>
<li>Bump com.fasterxml.jackson:jackson-bom from 2.22.0 to 2.22.1 <a href="">#19419</a></li>
<li>Bump com.fasterxml.jackson:jackson-bom from 2.22.1 to 2.22.2 <a href="">#19566</a></li>
<li>Bump com.nimbusds:oauth2-oidc-sdk from 11.37.2 to 11.38.1 <a href="">#19439</a></li>
<li>Bump com.nimbusds:oauth2-oidc-sdk from 11.38.1 to 11.38.2 <a href="">#19525</a></li>
<li>Bump com.unboundid:unboundid-ldapsdk from 7.0.4 to 7.0.5 <a href="">#19322</a></li>
<li>Bump com.webauthn4j:webauthn4j-core from 0.31.6.RELEASE to 0.31.7.RELEASE <a href="">#19313</a></li>
<li>Bump com.webauthn4j:webauthn4j-core from 0.31.7.RELEASE to 0.31.8.RELEASE <a href="">#19409</a></li>
<li>Bump com.webauthn4j:webauthn4j-core from 0.31.8.RELEASE to 0.31.9.RELEASE <a href="">#19496</a></li>
<li>Bump gradle-wrapper from 9.5.1 to 9.6.0 <a href="">#19360</a></li>
<li>Bump gradle-wrapper from 9.6.0 to 9.6.1 <a href="">#19393</a></li>
<li>Bump gradle-wrapper from 9.6.1 to 9.7.0 <a href="">#19516</a></li>
<li>Bump io.spring.nullability:io.spring.nullability.gradle.plugin from 0.0.13 to 0.0.14 <a href="">#19378</a></li>
<li>Bump org-bouncycastle from 1.84 to 1.85 <a href="">#19437</a></li>
<li>Bump org-jetbrains-kotlin from 2.4.0 to 2.4.10 <a href="">#19447</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>a825937</code></a> Release 7.1.1</li>
<li><a href=""><code>74c91f8</code></a> Update to Spring Data 2026.0.1</li>
<li><a href=""><code>b822214</code></a> Update to Spring LDAP 4.1.1</li>
<li><a href=""><code>39da00f</code></a> Update to Micrometer 1.17.1</li>
<li><a href=""><code>4be80b7</code></a> Update to Reactor 2025.0.7</li>
<li><a href=""><code>564a677</code></a> Update to Spring Framework 7.0.9</li>
<li><a href=""><code>2930198</code></a> Configure Build for Commercial Repositories</li>
<li><a href=""><code>25f9a91</code></a> Configure with Commercial Workflows</li>
<li><a href=""><code>bf8569f</code></a> Remove OSS CI configuration</li>
<li><a href=""><code>dcee218</code></a> Use jspecify Nullable in DPoPProofReplayValidator</li>
<li>Additional commits viewable in <a href="https://github.com/spring-projects/spring-security/compare/7.0.7...7.1.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.springframework.security:spring-security-bom&package-manager=maven&previous-version=7.0.7&new-version=7.1.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `be8716784e90`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.