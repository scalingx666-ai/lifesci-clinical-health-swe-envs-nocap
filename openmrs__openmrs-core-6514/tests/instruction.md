# Issue

**Title:** maven(deps): bump org.springframework:spring-test from 7.0.8 to 7.0.9

## Description

Bumps [org.springframework:spring-test](https://github.com/spring-projects/spring-framework) from 7.0.8 to 7.0.9.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/spring-projects/spring-framework/releases">org.springframework:spring-test's releases</a>.</em></p>
<blockquote>
<h2>v7.0.9</h2>
<h2>:warning: Attention Required</h2>
<ul>
<li>In Spring Framework 7.0.9, <code>ForwardedHeaderFilter</code> (Spring MVC) and <code>ForwardedHeaderTransformer</code> (WebFlux) each provide a boolean constructor argument whether to use the standard &quot;Forwarded&quot; header or the &quot;X-Forwarded&quot; alternative headers. A separate property turns on and off use of &quot;X-Forwarded-Prefix&quot;. While the default constructor preserves the existing behavior, we recommend to use the new constructor to explicitly specify which forwarded headers to use to make the processing more deterministic and aligned with what is expected from the proxy. Please, see the updated <a href="https://docs.spring.io/spring-framework/reference/7.0.9-SNAPSHOT/web/webmvc/filters.html#filters-forwarded-headers-security">Security Considerations</a> section for details. In 7.1 with <a href="">#37072</a> the default constructor is deprecated and marked for removal. <a href="">#37090</a></li>
<li>In Spring Framework 7.0.9, <code>SimpleEvaluationContext</code> no longer supports expression compilation by default, regardless of the compiler mode configured via <code>SpelParserConfiguration</code> or the <code>spring.expression.compiler.mode</code> system property or Spring property. Applications that intentionally use <code>SimpleEvaluationContext</code> with trusted expressions and require compilation for performance reasons can opt in by calling <code>withCompilationSupported()</code> on the <code>SimpleEvaluationContext</code> builder. Care should be taken when opting in to compilation, as doing so removes the safety guards applied during interpreted evaluation. <a href="">#37035</a></li>
</ul>
<h2>:star: New Features</h2>
<ul>
<li>Ignore an empty port value in URI parsing <a href="">#37117</a></li>
<li>Avoid retaining class files in annotation metadata <a href="">#37112</a></li>
<li>Add <code>@Nullable</code> annotations when treating <code>Map.remove()</code> as returning <code>@Nullable</code> <a href="">#37067</a></li>
<li>Revisit SSE view fragments handling <a href="">#37061</a></li>
<li>Check list index after auto-grow in <code>AbstractNestablePropertyAccessor</code> <a href="">#37036</a></li>
<li>Disable SpEL expression compilation by default in <code>SimpleEvaluationContext</code> <a href="">#37035</a></li>
<li>Limit result size of <code>BigDecimal</code>/<code>BigInteger</code> power operations in SpEL <a href="">#37034</a></li>
<li>Refactor redirect handling in UrlHandlerFilter <a href="">#37030</a></li>
<li>Revise stylesheet source handling in XsltView <a href="">#37029</a></li>
<li>Revise view name handling in UrlFilenameViewController <a href="">#37027</a></li>
<li>Handle pre-flight requests in functional endpoint setup without DispatcherHandler <a href="">#37024</a></li>
<li>Improve WebSocket handshake error logging <a href="">#37023</a></li>
<li>Fix missing nullability in JdbcTemplate.batchUpdate <a href="">#37012</a></li>
<li>Timeout property in RetryPolicy does not have a default constant <a href="">#36983</a></li>
<li>Write native configuration files as UTF-8 <a href="">#36972</a></li>
<li>DefaultServerRequest.ServletParametersMap.entrySet() does not retain HttpServletRequest.getParameterMap() order <a href="">#36966</a></li>
<li>Perform nextKey within synchronization for SQLite as well <a href="">#36959</a></li>
<li>Add support for custom ObjectInputFilter on DefaultDeserializer <a href="">#36958</a></li>
<li>Revise resource bundle caching for common locales <a href="">#36957</a></li>
<li>Improve nullability for <code>getSession(*)</code> in <code>MockHttpServletRequest</code> <a href="">#36926</a></li>
<li>Improve fallback logic in ParameterContentNegotiationStrategy and ParameterContentTypeResolver <a href="">#36925</a></li>
<li>Improve ambiguous match check on preflight request <a href="">#36903</a></li>
<li>Improve Groovy markup template loading <a href="">#36902</a></li>
<li>Improve request path handling on a Reactor Netty server <a href="">#36893</a></li>
<li>Improve JettyWebSocketSession error handling <a href="">#36891</a></li>
</ul>
<h2>:lady_beetle: Bug Fixes</h2>
<ul>
<li>EclipseLinkJpaDialect singleton lock in EclipseLinkConnectionHandle.getConnection() serializes all JDBC connection acquisitions under load <a href="">#37085</a></li>
<li>MetadataReader fails to read byte[] array from annotation <a href="">#37083</a></li>
<li>Ensure parsing/tostring symmetry in ContentDisposition <a href="">#37064</a></li>
<li>Character outside of permitted range in Content Disposition <a href="">#37062</a></li>
<li>Release Jackson BufferRecycler to its pool in encoders <a href="">#37059</a></li>
<li>Ensure consistent error escaping <a href="">#37055</a></li>
<li>Refine template name processing <a href="">#37054</a></li>
<li>Reset TwoByteMatcher partial match on mismatching byte <a href="">#37053</a></li>
<li>Refactor async XML parsing limit checks <a href="">#37031</a></li>
<li>Fix part constraint checks in PartEventHttpMessageReader <a href="">#37028</a></li>
<li>Fix buffer leak in RSocket SETUP frame handling <a href="">#37026</a></li>
<li>Ensure correct Jetty core response cookie handling <a href="">#37025</a></li>
<li>Align <code>domainToAscii</code> with current WhatWG spec <a href="">#37018</a></li>
<li>Ensure consistent <code>ButtonTag</code> value attribute processing <a href="">#37017</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>82a6b40</code></a> Release Spring Framework 7.0.9</li>
<li><a href=""><code>a7b1b59</code></a> Upgrade to Reactor 2025.0.7</li>
<li><a href=""><code>996e3d3</code></a> Upgrade to Micrometer 1.16.7</li>
<li><a href=""><code>73f5ddd</code></a> Refactor maxInMemory limit handling for async XML parsing</li>
<li><a href=""><code>675f25d</code></a> Leading slash handling in UrlHandlerFilter</li>
<li><a href=""><code>692dbc9</code></a> Apply ResourceHandlerUtils checks in XsltView</li>
<li><a href=""><code>8647e90</code></a> Consistent maxPartSize check in PartEventHttpMessageReader</li>
<li><a href=""><code>b9379e3</code></a> Check viewName for special prefixes in UrlFilenameViewController</li>
<li><a href=""><code>a784dbe</code></a> Ensure Payload release on early error in createHeaders</li>
<li><a href=""><code>3b492f3</code></a> Return sameSite cookie value in Jetty response</li>
<li>Additional commits viewable in <a href="https://github.com/spring-projects/spring-framework/compare/v7.0.8...v7.0.9">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.springframework:spring-test&package-manager=maven&previous-version=7.0.8&new-version=7.0.9)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7ec569f4849c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.