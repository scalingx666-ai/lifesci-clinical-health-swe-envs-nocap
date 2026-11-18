# Issue

**Title:** maven(deps): bump io.netty:netty-bom from 4.2.16.Final to 4.2.17.Final

## Description

Bumps [io.netty:netty-bom](https://github.com/netty/netty) from 4.2.16.Final to 4.2.17.Final.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/netty/netty/releases">io.netty:netty-bom's releases</a>.</em></p>
<blockquote>
<h2>netty-4.2.17.Final</h2>
<h2>What's Changed</h2>
<ul>
<li>AsciiString.cached(String) should sanitize the provided String (<a href="">#13749</a>) by <a href="https://github.com/vpelikh"><code>@​vpelikh</code></a> in <a href="">netty/netty#17007</a></li>
<li>Fix deploy workflow by <a href="https://github.com/normanmaurer"><code>@​normanmaurer</code></a> in <a href="">netty/netty#17071</a></li>
<li>Fix AsciiString.cached(String) performance regression by <a href="https://github.com/dreamlike-ocean"><code>@​dreamlike-ocean</code></a> in <a href="">netty/netty#17074</a></li>
<li>SslHandler: Fix possible buffer leak when an OOME is thrown during allocation by <a href="https://github.com/normanmaurer"><code>@​normanmaurer</code></a> in <a href="">netty/netty#17059</a></li>
<li>Avoid leak presence detector in leak profile by <a href="https://github.com/yawkat"><code>@​yawkat</code></a> in <a href="">netty/netty#17073</a></li>
<li>Add HttpContentCompressor constructor with ability to specify desired maxPipelineDepth by <a href="https://github.com/reta"><code>@​reta</code></a> in <a href="">netty/netty#17068</a></li>
<li>IoUring: preserve readPending when rescheduling cancelled reads by <a href="https://github.com/dreamlike-ocean"><code>@​dreamlike-ocean</code></a> in <a href="">netty/netty#17087</a></li>
<li>Reject negative maxOrder in PooledByteBufAllocator by <a href="https://github.com/coderbruis"><code>@​coderbruis</code></a> in <a href="">netty/netty#17093</a></li>
<li>Fix AdaptiveByteBuf._setLongLE calling checked setLongLE by <a href="https://github.com/franz1981"><code>@​franz1981</code></a> in <a href="">netty/netty#17098</a></li>
<li>Snappy: Guard decoder against invalid chunk lengths by <a href="https://github.com/yawkat"><code>@​yawkat</code></a> in <a href="">netty/netty#17099</a></li>
<li>Fix OCSP Tests by <a href="https://github.com/chrisvest"><code>@​chrisvest</code></a> in <a href="">netty/netty#17114</a></li>
<li>Update to latest netty-tcnative release by <a href="https://github.com/normanmaurer"><code>@​normanmaurer</code></a> in <a href="">netty/netty#17056</a></li>
<li>Use safe decompressor in Lz4FrameDecoder by <a href="https://github.com/yawkat"><code>@​yawkat</code></a> in <a href="">netty/netty#17118</a></li>
<li>Configure TestLens for the PR builds by <a href="https://github.com/chrisvest"><code>@​chrisvest</code></a> in <a href="">netty/netty#17129</a></li>
<li>IoUring: add SO_INQ support for Unix domain sockets by <a href="https://github.com/dreamlike-ocean"><code>@​dreamlike-ocean</code></a> in <a href="">netty/netty#17127</a></li>
<li>fix(mqtt): drop UNSUBACK reason codes for MQTT 3.x encoding by <a href="https://github.com/ChunMengLu"><code>@​ChunMengLu</code></a> in <a href="">netty/netty#17117</a></li>
<li>Propagate the CI envionment variables through to the docker builds by <a href="https://github.com/chrisvest"><code>@​chrisvest</code></a> in <a href="">netty/netty#17138</a></li>
<li>Codec-compression: Add decompressor API by <a href="https://github.com/yawkat"><code>@​yawkat</code></a> in <a href="">netty/netty#16745</a></li>
<li>Fix silent failures and optimize error short-circuit in multi-threaded tests by <a href="https://github.com/rajan-github"><code>@​rajan-github</code></a> in <a href="">netty/netty#17106</a></li>
<li>Codec-compression: Add Bzip2Decompressor by <a href="https://github.com/yawkat"><code>@​yawkat</code></a> in <a href="">netty/netty#17145</a></li>
<li>Fix buddy cache evicting chunks with live buffers by <a href="https://github.com/franz1981"><code>@​franz1981</code></a> in <a href="">netty/netty#17154</a></li>
<li>Codec-compression: Add Snappy frame decompressor by <a href="https://github.com/yawkat"><code>@​yawkat</code></a> in <a href="">netty/netty#17153</a></li>
<li>Codec-compression: Add zlib decompressors by <a href="https://github.com/yawkat"><code>@​yawkat</code></a> in <a href="">netty/netty#17155</a></li>
<li>Codec-compression: Add Zstd decompressor by <a href="https://github.com/yawkat"><code>@​yawkat</code></a> in <a href="">netty/netty#17152</a></li>
<li>Codec-compression: Add LZF decompressor by <a href="https://github.com/yawkat"><code>@​yawkat</code></a> in <a href="">netty/netty#17147</a></li>
<li>Codec-compression: Add BrotliDecompressor by <a href="https://github.com/yawkat"><code>@​yawkat</code></a> in <a href="">netty/netty#17146</a></li>
<li>Codec-compression: Add Lz4FrameDecompressor by <a href="https://github.com/yawkat"><code>@​yawkat</code></a> in <a href="">netty/netty#17148</a></li>
<li><code>HttpObjectEncoder</code> / <code>DefaultHttp2FrameWriter</code>: fix buffer leak when a <code>Throwable</code> is thrown during header encoding by <a href="https://github.com/HwangRock"><code>@​HwangRock</code></a> in <a href="">netty/netty#17089</a></li>
<li>Fix direct memory OOM on low-core containers by <a href="https://github.com/franz1981"><code>@​franz1981</code></a> in <a href="">netty/netty#17166</a></li>
<li>IoUring: Fix the recvmmsg emulation by <a href="https://github.com/dreamlike-ocean"><code>@​dreamlike-ocean</code></a> in <a href="">netty/netty#17187</a></li>
<li>Avoid classloader leak via GlobalEventExecutor terminationFuture failure by <a href="https://github.com/seonwooj0810"><code>@​seonwooj0810</code></a> in <a href="">netty/netty#17140</a></li>
<li>BrotliEncoder: Prevent duplicate close scheduling by <a href="https://github.com/yawkat"><code>@​yawkat</code></a> in <a href="">netty/netty#17175</a></li>
<li>Fix JdkZlibDecompressor losing the tail of highly compressible streams by <a href="https://github.com/renechoi"><code>@​renechoi</code></a> in <a href="">netty/netty#17191</a></li>
<li>Update compress-lzf to 1.2.1 by <a href="https://github.com/yawkat"><code>@​yawkat</code></a> in <a href="">netty/netty#17194</a></li>
<li>Do not write WebSocket handshake response to the tail of the pipeline by <a href="https://github.com/el-psy-kongroo-d"><code>@​el-psy-kongroo-d</code></a> in <a href="">netty/netty#17192</a></li>
<li><code>HttpServerCodec</code>: do not consume the method queue for 1xx interim responses by <a href="https://github.com/HwangRock"><code>@​HwangRock</code></a> in <a href="">netty/netty#17182</a></li>
<li>Weakly reference engines from the OpenSSL engine map by <a href="https://github.com/bryce-anderson"><code>@​bryce-anderson</code></a> in <a href="">netty/netty#17199</a></li>
<li>OpenSSL: Allow to obtain used named group via OpenSslSession by <a href="https://github.com/normanmaurer"><code>@​normanmaurer</code></a> in <a href="">netty/netty#17058</a></li>
<li>Add <code>.editorconfig</code> to enforce consistent coding style by <a href="https://github.com/vpelikh"><code>@​vpelikh</code></a> in <a href="">netty/netty#17052</a></li>
<li>Update surefire plugin to latest version by <a href="https://github.com/normanmaurer"><code>@​normanmaurer</code></a> in <a href="">netty/netty#17210</a></li>
<li>Merge changes from forks by <a href="https://github.com/chrisvest"><code>@​chrisvest</code></a> in <a href="">netty/netty#17213</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/vpelikh"><code>@​vpelikh</code></a> made their first contribution in <a href="">netty/netty#17007</a></li>
<li><a href="https://github.com/ChunMengLu"><code>@​ChunMengLu</code></a> made their first contribution in <a href="">netty/netty#17117</a></li>
<li><a href="https://github.com/rajan-github"><code>@​rajan-github</code></a> made their first contribution in <a href="">netty/netty#17106</a></li>
<li><a href="https://github.com/seonwooj0810"><code>@​seonwooj0810</code></a> made their first contribution in <a href="">netty/netty#17140</a></li>
<li><a href="https://github.com/renechoi"><code>@​renechoi</code></a> made their first contribution in <a href="">netty/netty#17191</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>e0789d3</code></a> [maven-release-plugin] prepare release netty-4.2.17.Final</li>
<li><a href=""><code>1b5abc6</code></a> Merge changes from forks (<a href="">#17213</a>)</li>
<li><a href=""><code>36fbf57</code></a> Update surefire plugin to latest version (<a href="">#17210</a>)</li>
<li><a href=""><code>a96226c</code></a> Add <code>.editorconfig</code> to enforce consistent coding style (<a href="">#17052</a>)</li>
<li><a href=""><code>14a4e6a</code></a> OpenSSL: Allow to obtain used named group via OpenSslSession (<a href="">#17058</a>)</li>
<li><a href=""><code>26255b1</code></a> Weakly reference engines from the OpenSSL engine map (<a href="">#17199</a>)</li>
<li><a href=""><code>ae41417</code></a> <code>HttpServerCodec</code>: do not consume the method queue for 1xx interim responses ...</li>
<li><a href=""><code>41f1db5</code></a> Do not write WebSocket handshake response to the tail of the pipeline (<a href="">#17192</a>)</li>
<li><a href=""><code>035d76e</code></a> Update compress-lzf to 1.2.1 (<a href="">#17194</a>)</li>
<li><a href=""><code>7681aff</code></a> Fix JdkZlibDecompressor losing the tail of highly compressible streams (<a href="">#17191</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/netty/netty/compare/netty-4.2.16.Final...netty-4.2.17.Final">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=io.netty:netty-bom&package-manager=maven&previous-version=4.2.16.Final&new-version=4.2.17.Final)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1c71dca2e9cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.