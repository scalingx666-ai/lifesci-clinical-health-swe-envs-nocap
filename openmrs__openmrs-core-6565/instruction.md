# Issue

**Title:** maven(deps): bump io.netty:netty-bom from 4.2.17.Final to 4.2.18.Final

## Description

Bumps [io.netty:netty-bom](https://github.com/netty/netty) from 4.2.17.Final to 4.2.18.Final.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/netty/netty/releases">io.netty:netty-bom's releases</a>.</em></p>
<blockquote>
<h2>netty-4.2.18.Final</h2>
<h2>Security fixes</h2>
<ul>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-rmcw-9fcq-wjq7">CVE-2026-XXXXX</a> : unbounded resource usage in <code>io.netty:netty-codec-http</code> (SPDY)</li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-pvjx-v7vp-62vq">CVE-2026-XXXXX</a> : unbounded resource usage in <code>io.netty:netty-codec-http</code> (HTTP/1.1)</li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-8352-h356-c9qh">CVE-2026-XXXXX</a> : denial of service vector in <code>io.netty:netty-codec-http2</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-jj3c-mwvr-9g52">CVE-2026-XXXXX</a> : improper certificate validation in <code>io.netty:netty-handler-ssl-ocsp</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-ghg5-c4jg-8q5j">CVE-2026-XXXXX</a> : memory leak in <code>io.netty:netty-codec-stomp</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-2g37-3h88-55hc">CVE-2026-XXXXX</a> : unbounded resource usage in <code>io.netty:netty-codec-http</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-q9pg-8h3j-8hvm">CVE-2026-XXXXX</a> : improper header validation in <code>io.netty:netty-codec-http3</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-hmf3-49g9-g7qq">CVE-2026-XXXXX</a> : denial of service vector in <code>io.netty:netty-codec-stomp</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-wxrh-4rgq-pjcg">CVE-2026-XXXXX</a> : parser desync/response smuggling in <code>io.netty:netty-codec-memcache</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-495p-pchh-r4mc">CVE-2026-XXXXX</a> : unbounded resource usage in <code>io.netty:netty-codec-http3</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-v5p2-hmgx-3xrx">CVE-2026-XXXXX</a> : unbounded resource usage in <code>io.netty:netty-codec-http3</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-f64r-x647-cg8w">CVE-2026-XXXXX</a> : unbounded resource usage in <code>io.netty:netty-codec-http3</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-hcvj-94mj-jp5c">CVE-2026-XXXXX</a> : improper header validation in <code>io.netty:netty-codec-http</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-pq4x-537v-r54q">CVE-2026-XXXXX</a> : unbounded resource usage in <code>io.netty:netty-codec-smtp</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-j58c-g352-8h4p">CVE-2026-XXXXX</a> : memory leak in <code>io.netty:netty-codec-haproxy</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-h75q-xqrh-59rf">CVE-2026-XXXXX</a> : request smuggling in <code>io.netty:netty-codec-http</code> (RTSP)</li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-rq4j-fc47-9698">CVE-2026-XXXXX</a> : request smuggling in <code>io.netty:netty-codec-http</code> (HTTP/1)</li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-45h4-vhwh-fmhg">CVE-2026-XXXXX</a> : improper header validation in <code>io.netty:netty-codec-http2</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-jgph-cgq3-c627">CVE-2026-XXXXX</a> : improper header validation in <code>io.netty:netty-codec-http</code> (HTTP/1)</li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-hfr2-x62w-v49h">CVE-2026-XXXXX</a> : improper header validation in <code>io.netty:netty-codec-http3</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-w6j8-x45j-w75f">CVE-2026-XXXXX</a> : improper header validation in <code>io.netty:netty-codec-http3</code> and in <code>io.netty:netty-codec-http2</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-cg2g-fxr4-mg8m">CVE-2026-XXXXX</a> : improper header validation in <code>io.netty:netty-codec-http2</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-mj35-3qqm-q387">CVE-2026-XXXXX</a> : improper hostname verification in <code>io.netty:netty-codec-classes-quic</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-r4xx-7fpg-j8xg">CVE-2026-XXXXX</a> : unbounded resource usage in <code>io.netty:netty-codec-redis</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-3jrc-fchc-59pw">CVE-2026-XXXXX</a> : improper header validation in <code>io.netty:netty-codec-http</code> (HTTP/1.1)</li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-j4mg-hqgv-34qc">CVE-2026-XXXXX</a> : request smuggling vector in <code>io.netty:netty-codec-http</code> (HTTP/1.1)</li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-jqf3-r9ww-c5x8">CVE-2026-XXXXX</a> : unbounded resource usage in <code>io.netty:netty-codec-mqtt</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-5vh9-c45f-rf7p">CVE-2026-XXXXX</a> : improper CRLF neutralization in <code>io.netty:netty-codec-smtp</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-jhjp-5q4f-8wr2">CVE-2026-XXXXX</a> : improper certificate validation in <code>io.netty:netty-handler-ssl-ocsp</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-8whp-c7w8-2m72">CVE-2026-XXXXX</a> : improper header validation in <code>io.netty:netty-codec-http2</code></li>
</ul>
<h2>Compatibility Notes</h2>
<p>A number of security fixes have added additional validation and impose new resource usage limits, which may cause existing workloads to fail or be rejected. We recommend that you test your systems thoroughly as part of your Netty upgrade.</p>
<p>Two specific changes are worth calling out:</p>
<p><strong>QUIC now explicitly requires <code>X509ExtendedTrustManager</code> when hostname verification is enabled.</strong>
Previously, when configuring QUIC with an endpoint identification algorithm and an <code>X509TrustManager</code>, hostname verification would be silently skipped.
This is now considered a misconfiguration and an exception will be thrown.</p>
<p><strong>HTTP/2 header <em>value</em> validation is now enabled by default.</strong>
HTTP/2 header <em>name</em> validation has always been enabled by default, with an option to disable it, but HTTP/2 header <em>value</em> validation has been disabled by default until now. Configuration options still exist to disable this, but validation of HTTP header names and values are now both opt-in by default rather than opt-out.</p>
<h2>What's Changed</h2>
<ul>
<li>Use X509ExtendedTrustManager in SSLErrorTest by <a href="https://github.com/normanmaurer"><code>@​normanmaurer</code></a> in <a href="">netty/netty#17221</a></li>
<li>Update setup-testlens to v1.9.4 by <a href="https://github.com/marcphilipp"><code>@​marcphilipp</code></a> in <a href="">netty/netty#17223</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>2521f49</code></a> [maven-release-plugin] prepare release netty-4.2.18.Final</li>
<li><a href=""><code>6fd5327</code></a> HTTP/1 absolute-form Host mismatch is translated to HTTP/3 :authority, overri...</li>
<li><a href=""><code>c44a052</code></a> SPDY: SpdySessionHandler must limit the concurrent streams</li>
<li><a href=""><code>374d965</code></a> HTTP: Limit the maximum number of concurrent pipelined requests</li>
<li><a href=""><code>7e8b325</code></a> HTTP/2: Limit HPACK encoding table size</li>
<li><a href=""><code>e3ebf70</code></a> OCSP: Correctly handle that <code>nextUpdate</code> is optional</li>
<li><a href=""><code>5388535</code></a> STOMP: Correctly release partial content on handler removal</li>
<li><a href=""><code>3a80f5a</code></a> WebSockets: Enforce a limit for the max pipelined requests in WebSocketServer...</li>
<li><a href=""><code>1b6ea48</code></a> HTTP3: Correctly handle &quot;:authority&quot; and &quot;host&quot; headers</li>
<li><a href=""><code>3630659</code></a> STOMP codec content-length long-to-int truncation causes infinite decode loop...</li>
<li>Additional commits viewable in <a href="https://github.com/netty/netty/compare/netty-4.2.17.Final...netty-4.2.18.Final">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=io.netty:netty-bom&package-manager=maven&previous-version=4.2.17.Final&new-version=4.2.18.Final)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f06c26ac7b79`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.