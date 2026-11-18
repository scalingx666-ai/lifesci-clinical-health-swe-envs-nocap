# Issue

**Title:** maven(deps): bump io.netty:netty-bom from 4.2.18.Final to 4.2.19.Final

## Description

Bumps [io.netty:netty-bom](https://github.com/netty/netty) from 4.2.18.Final to 4.2.19.Final.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/netty/netty/releases">io.netty:netty-bom's releases</a>.</em></p>
<blockquote>
<h2>netty-4.2.19.Final</h2>
<h2>Security</h2>
<p><strong>Note that <a href="https://netty.io/news/2026/09/09/4-1-EOL-announcement.html">Netty 4.1 will be End-of-Life on July 1st, 2027</a>.</strong></p>
<p>We strongly recommend upgrading to this version to get the following security fixes:</p>
<ul>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-frq3-7pw6-36cg">CVE-2026-XXXXX</a> : parser desync in <code>io.netty:netty-codec-haproxy</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-6g26-xhvx-g5w3">CVE-2026-XXXXX</a> : improper CRLF neutralization (request/response smuggling) in <code>io.netty:netty-codec-http</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-x9f7-rg73-4rp6">CVE-2026-XXXXX</a> : origin validation error in <code>io.netty:netty-codec-http</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-2p3h-phr9-jf38">CVE-2026-XXXXX</a> : unbounded resource consumption in <code>io.netty:netty-codec-http2</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-vwgc-hvc9-2j59">CVE-2026-XXXXX</a> : request/response smuggling in <code>io.netty:netty-codec-http</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-m3w2-2657-46g8">CVE-2026-XXXXX</a> : time-of-check/time-of-use error in <code>io.netty:netty-handler-ssl-ocsp</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-jp47-57pp-4qpp">CVE-2026-XXXXX</a> : SNI routing bypass in <code>io.netty:netty-handler</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-35qr-v9mm-35c5">CVE-2026-XXXXX</a> : unbounded resource consumption in <code>io.netty:netty-codec-xml</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-5h6f-wp3f-6hmv">CVE-2026-XXXXX</a> : unbounded resource consumption in <code>io.netty:netty-codec-base</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-x436-m93c-g2q9">CVE-2026-XXXXX</a> : unbounded resource consumption in <code>io.netty:netty-codec-http</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-c7hc-m259-xhcr">CVE-2026-XXXXX</a> : input misinterpretation in <code>io.netty:netty-codec-socks</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-268p-9r42-7qp4">CVE-2026-XXXXX</a> : improper access control in <code>io.netty:netty-handler</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-3h79-3wcf-5whr">CVE-2026-XXXXX</a> : unbounded resource consumption in <code>io.netty:netty-codec-dns</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-25w5-4jgp-m94q">CVE-2026-XXXXX</a> : unbounded resource consumption in <code>io.netty:netty-codec-http3</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-x2j7-6j3j-5vwj">CVE-2026-XXXXX</a> : use-after-free in <code>io.netty:netty-transport-classes-io_uring</code></li>
<li><a href="https://github.com/netty/netty/security/advisories/GHSA-79q2-mhf4-2j6j">CVE-2026-XXXXX</a> : memory leak in <code>io.netty:netty-transport-native-io_uring</code></li>
</ul>
<p>Note that due to overwhelming strain on the CVE infrastructure, we have not gotten a single CVE number assigned to these reports in time for our release.
The advisories will be published without.</p>
<p>Specific changes worth calling out:</p>
<p><strong>Validation in <code>FileUpload.setContentType</code>.</strong>
Previously, the <code>FileUpload.setContentType</code> methods did not validate their inputs.
They now throw an <code>IllegaalArgumentException</code> if the given string is not formatted as a plausible MIME content type.</p>
<h2>What's Changed</h2>
<ul>
<li>perf: Use LinkedHashSet to deduplicate search domains by <a href="https://github.com/JunggiKim"><code>@​JunggiKim</code></a> in <a href="">netty/netty#17400</a></li>
<li>Handle non-positive skip lengths in ByteBufInputStream by <a href="https://github.com/cuishuang"><code>@​cuishuang</code></a> in <a href="">netty/netty#17388</a></li>
<li>Avoid double promise allocation in SslHandler.wrap() by <a href="https://github.com/doom369"><code>@​doom369</code></a> in <a href="">netty/netty#17382</a></li>
<li>Socket: Add half-closure tests to SocketHalfClosedTest by <a href="https://github.com/rajan-github"><code>@​rajan-github</code></a> in <a href="">netty/netty#17394</a></li>
<li>HttpUtil.getCharset() must accept whitespace before the next Content-Type parameter by <a href="https://github.com/hunseonglee"><code>@​hunseonglee</code></a> in <a href="">netty/netty#17386</a></li>
<li>codec-dns: Add SMIMEA, CDS, CDNSKEY, OPENPGPKEY, CSYNC, ZONEMD records by <a href="https://github.com/hyperxpro"><code>@​hyperxpro</code></a> in <a href="">netty/netty#17373</a></li>
<li>transport: Avoid io_uring completion callback allocation by <a href="https://github.com/massiccio"><code>@​massiccio</code></a> in <a href="">netty/netty#17457</a></li>
<li>QUIC: Ensure writable events reflect stream capacity by <a href="https://github.com/yawkat"><code>@​yawkat</code></a> in <a href="">netty/netty#17431</a></li>
<li>OcspServerCertificateValidatorTest: Fix possible leak in test by <a href="https://github.com/normanmaurer"><code>@​normanmaurer</code></a> in <a href="">netty/netty#17469</a></li>
<li>Use github to download cmake and also remove tar file after unpacking by <a href="https://github.com/normanmaurer"><code>@​normanmaurer</code></a> in <a href="">netty/netty#17482</a></li>
<li>build: Upgrade GitHub Actions to fix Node.js 20 deprecation warnings by <a href="https://github.com/normanmaurer"><code>@​normanmaurer</code></a> in <a href="">netty/netty#17484</a></li>
<li>HttpUtil.getMimeType() must not include whitespace before the next Content-Type parameter by <a href="https://github.com/ohchanKyu"><code>@​ohchanKyu</code></a> in <a href="">netty/netty#17456</a></li>
<li>Fix buffer leak when recvmmsg returns single UDP_GRO batch by <a href="https://github.com/octa-one"><code>@​octa-one</code></a> in <a href="">netty/netty#17493</a></li>
<li>Guard ChunkedWriteHandler.doFlush() against re-entrant invocation from user code by <a href="https://github.com/fudianchn"><code>@​fudianchn</code></a> in <a href="">netty/netty#17438</a></li>
<li>Add regression test for close() cascade reentering flush() by <a href="https://github.com/normanmaurer"><code>@​normanmaurer</code></a> in <a href="">netty/netty#17497</a></li>
<li>Fix UDP_GRO segment size is lost when reading with recvmmsg by <a href="https://github.com/octa-one"><code>@​octa-one</code></a> in <a href="">netty/netty#17492</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>64cc10f</code></a> [maven-release-plugin] prepare release netty-4.2.19.Final</li>
<li><a href=""><code>e863e69</code></a> Fix io_uring domain socket fd leak on multi-fd SCM_RIGHTS messages</li>
<li><a href=""><code>d82c6c3</code></a> Fix IP allow-list bypass from ruleType-blind dedup in IpSubnetFilter</li>
<li><a href=""><code>bccc62a</code></a> Bound domain-name decode buffer to avoid quadratic allocation</li>
<li><a href=""><code>6b02cd3</code></a> Fix wrong nextBid computation in IoUringBufferRing for RECVSEND_BUNDLE</li>
<li><a href=""><code>ef3a3e1</code></a> Fix sign-extension bug in SocksInitRequestDecoder NMETHODS field</li>
<li><a href=""><code>4cacdf0</code></a> Fix quadratic CPU usage in XmlFrameDecoder when an element is never balanced</li>
<li><a href=""><code>20f3aae</code></a> Fail closed on zero-length handshake records in SslClientHelloHandler</li>
<li><a href=""><code>c3f7088</code></a> Netty OcspServerCertificateValidator still delivers buffered data from a revo...</li>
<li><a href=""><code>4029f07</code></a> Correctly handle multiple Content-Length</li>
<li>Additional commits viewable in <a href="https://github.com/netty/netty/compare/netty-4.2.18.Final...netty-4.2.19.Final">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=io.netty:netty-bom&package-manager=maven&previous-version=4.2.18.Final&new-version=4.2.19.Final)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a69b14a84bf9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.