# Issue

**Title:** maven(deps): bump org.postgresql:postgresql from 42.7.13 to 42.7.14

## Description

Bumps [org.postgresql:postgresql](https://github.com/pgjdbc/pgjdbc) from 42.7.13 to 42.7.14.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pgjdbc/pgjdbc/releases">org.postgresql:postgresql's releases</a>.</em></p>
<blockquote>
<h2>v42.7.14</h2>
<h2>Security</h2>
<p>This release fixes two security vulnerabilities.</p>
<h3><code>requireAuth</code> is silently not enforced when the value excludes every authentication method (<a href="https://github.com/pgjdbc/pgjdbc/security/advisories/GHSA-rhp9-mr79-r74h">GHSA-rhp9-mr79-r74h</a>, CVE-2026-107314)</h3>
<p><strong>Severity:</strong> Moderate (CVSS 5.9) | <strong>Affected versions:</strong> 42.7.11 – 42.7.13</p>
<p>If the <code>requireAuth</code> connection property excluded all six authentication methods the driver knows (for example <code>requireAuth=!password,!md5,!gss,!sspi,!scram-sha-256,!none</code>) or contained no method at all (for example <code>requireAuth=,</code>), the driver applied no restriction and accepted whatever method the server asked for, including cleartext <code>password</code>. An attacker positioned between the application and the server could use this to request cleartext password authentication and receive the database password.</p>
<p>Unset values, positive lists (such as <code>requireAuth=scram-sha-256</code>) and partial exclusions (such as <code>requireAuth=!password,!md5</code>) were not affected, and neither were deployments that do not set <code>requireAuth</code>.</p>
<p>Behavior after upgrading:</p>
<ul>
<li>A value that excludes every method now refuses the connection with SQLState <code>08004</code> and the message <code>Authentication method is not allowed by requireAuth</code> (or the channel binding error when <code>channelBinding=require</code> is also set).</li>
<li>A value that names no method is rejected as an invalid <code>requireAuth</code> value.</li>
</ul>
<p>Because affected deployments had this value by mistake, and connections worked normally on affected versions, <strong>connections with such a value will fail after upgrading</strong>. Replace it with a positive list of the methods your server uses, for example <code>requireAuth=scram-sha-256</code>.</p>
<p>Independently of this fix, use <code>sslmode=verify-full</code> with a trusted CA so that an attacker cannot present a substitute server.</p>
<p>Thanks to <a href="https://github.com/manus-pi"><code>@​manus-pi</code></a> for finding and reporting this issue.</p>
<h3>Driver stores bytes of earlier statements when it pads a value shorter than its declared length (<a href="https://github.com/pgjdbc/pgjdbc/security/advisories/GHSA-f64h-wr5q-3qf3">GHSA-f64h-wr5q-3qf3</a>, CVE-2026-107315)</h3>
<p><strong>Severity:</strong> Moderate (CVSS 5.3) | <strong>Affected versions:</strong> 42.7.4 – 42.7.13</p>
<p>When an application sent a value shorter than the length it declared, the driver padded the missing bytes with data from earlier messages on the same connection instead of zeros, and the server stored them. The stored value could contain SQL text and parameter values of earlier, unrelated statements (up to 8192 bytes, or 16320 with GSS encryption). On pooled connections, those statements could come from other requests. 42.7.3 and earlier padded with zeros.</p>
<p>This is reachable through the following public API when the declared length is larger than the data:</p>
<ul>
<li><code>PreparedStatement.setObject(int, ByteStreamWriter)</code></li>
<li><code>CopyIn.writeToCopy(ByteStreamWriter)</code> and <code>CopyIn.writeToCopy(byte[], int, int)</code></li>
<li><code>PGCopyOutputStream.write(byte[], int, int)</code> (writes over 64 KiB)</li>
<li><code>LargeObject.write(byte[], int, int)</code></li>
<li><code>java.sql.Blob.setBytes(long, byte[], int, int)</code></li>
</ul>
<p>Padding is now always zeros. Applications whose declared length always matches the data were not affected. Values stored by an affected version through such a call may already contain leaked data, so you may want to review affected columns. There is no connection property to disable the old behavior; the workaround on older versions is to make the declared length match the data.</p>
<p>Thanks to <a href="https://github.com/vlsi"><code>@​vlsi</code></a> for finding and reporting this issue.</p>
<p><strong>Full Changelog</strong>: <a href="https://github.com/pgjdbc/pgjdbc/compare/REL42.7.13...REL42.7.14">https://github.com/pgjdbc/pgjdbc/compare/REL42.7.13...REL42.7.14</a></p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/pgjdbc/pgjdbc/blob/master/CHANGELOG.md">org.postgresql:postgresql's changelog</a>.</em></p>
<blockquote>
<h1>Changelog</h1>
<p>Notable changes since version 42.0.0, read the complete <a href="https://jdbc.postgresql.org/documentation/changelog.html">History of Changes</a>.</p>
<p>The format is based on <a href="http://keepachangelog.com/en/1.0.0/">Keep a Changelog</a>.</p>
<h2>[Unreleased]</h2>
<h3>Fixed</h3>
<ul>
<li>fix: <code>PGStream.skip</code> no longer loops forever when the connection ends while the driver is discarding bytes, and no longer mistakes a stream that skips nothing for one that has ended. <code>InputStream.skip</code> may return zero with more data still coming, which a stream supplied through the <code>socketFactory</code> property is free to do; the driver now reads a byte in that case and treats only <code>-1</code> as the end [PR <a href="">#4358</a>](<a href="">pgjdbc/pgjdbc#4358</a>)</li>
<li>fix: <code>LargeObjectManager</code> operations now work inside an active XA transaction. Since 42.7.13 an XA branch keeps the caller's <code>autoCommit=true</code>, and the guard rejected large objects as if the connection were idle. It now checks the server transaction state (<code>getTransactionState()</code>) instead of <code>autoCommit</code>, so a genuine auto-commit connection with no open transaction is still refused [Issue <a href="">#4309</a>](<a href="">pgjdbc/pgjdbc#4309</a>) [PR <a href="">#4310</a>](<a href="">pgjdbc/pgjdbc#4310</a>)</li>
<li>fix: batch update counts are no longer secured as committed inside an XA transaction. <code>BatchResultHandler</code> treated per-statement progress as durable whenever <code>autoCommit=true</code>, but an XA branch keeps <code>autoCommit=true</code> while the transaction is open, so a batch that flushed mid-way and then failed could report rolled-back statements as succeeded. Progress is now secured only when no server transaction is open [Issue <a href="">#4309</a>](<a href="">pgjdbc/pgjdbc#4309</a>) [PR <a href="">#4311</a>](<a href="">pgjdbc/pgjdbc#4311</a>)</li>
</ul>
<h3>Changed</h3>
<ul>
<li>fix: backend message lengths are checked before anything is sized from them. Each length is checked against the message layout and a limit for its type, the lengths inside <code>DataRow</code> and <code>FunctionCallResponse</code> are checked against the message, and the <code>NegotiateProtocolVersion</code> option count is bounded. A hostile or out of sync backend could previously force an allocation of up to two gigabytes with a five byte header [Issue <a href="">#4015</a>](<a href="">pgjdbc/pgjdbc#4015</a>)</li>
<li>fix: the read buffer is limited to 32 MiB and grows once per request rather than once per socket read. It previously doubled on every read while a large request was outstanding, so a peer that declared a large length and sent it slowly grew the buffer until the doubling past 1 GiB overflowed to a negative size [Issue <a href="">#4015</a>](<a href="">pgjdbc/pgjdbc#4015</a>)</li>
<li>fix: a zero-length <code>CopyData</code> body is accepted. It is valid on the wire and was previously rejected by an assertion, so it failed only on JVMs started with <code>-ea</code> [Issue <a href="">#4015</a>](<a href="">pgjdbc/pgjdbc#4015</a>)</li>
<li>fix: GSS packet lengths are bounded. The encrypted transport is limited to a 16380 byte payload and the handshake to a 65532 byte token, matching <code>PQ_GSS_MAX_PACKET_SIZE</code> and <code>PQ_GSS_AUTH_BUFFER_SIZE</code> [Issue <a href="">#4015</a>](<a href="">pgjdbc/pgjdbc#4015</a>)</li>
<li>fix: a connection whose stream has been refused is no longer reusable. Any refused length or count marks the stream broken, so <code>Connection.isClosed()</code> reports it closed and a pool that tests on borrow discards it. The socket is dropped with <code>SO_LINGER 0</code> [Issue <a href="">#4015</a>](<a href="">pgjdbc/pgjdbc#4015</a>)</li>
<li>fix: a protocol violation before authentication is reported as <code>PSQLException</code> with SQLState <code>08P01</code> rather than as a plain I/O error, and is no longer retried under <code>sslMode=allow</code> or <code>sslMode=prefer</code> [Issue <a href="">#4015</a>](<a href="">pgjdbc/pgjdbc#4015</a>)</li>
<li>fix: the counts inside <code>RowDescription</code>, <code>ParameterDescription</code>, <code>CopyInResponse</code> and <code>CopyOutResponse</code> are checked against the declared message length. A <code>RowDescription</code> claiming more fields than its length can hold previously read its field descriptions out of the messages that followed it [Issue <a href="">#4015</a>](<a href="">pgjdbc/pgjdbc#4015</a>)</li>
<li>fix: the driver checks that each backend message was consumed exactly before reading the next message type, so a reader that stops short of its declared length is refused rather than misreading what follows [Issue <a href="">#4015</a>](<a href="">pgjdbc/pgjdbc#4015</a>)</li>
<li>fix: the authentication loop, the GSS encryption handshake and the GSS authentication handshake each stop after 64 round trips. A zero-length GSS token is a valid continuation, so a server could previously keep a client exchanging tokens forever before any credentials were exchanged [Issue <a href="">#4015</a>](<a href="">pgjdbc/pgjdbc#4015</a>)</li>
<li>fix: <code>ErrorResponse</code> before authentication is limited to 30000 bytes rather than 32 MiB, matching libpq's limit for messages outside <code>VALID_LONG_MESSAGE_TYPE</code>, and a C string inside a declared message is no longer scanned past the end of that message. Both were allocations an unauthenticated peer could cause [Issue <a href="">#4015</a>](<a href="">pgjdbc/pgjdbc#4015</a>)</li>
<li>fix: an <code>ErrorResponse</code> or <code>NoticeResponse</code> longer than 32 MiB is truncated to that size rather than refused. The body past the limit is drained and the shortened message is delivered, so the connection stays usable [Issue <a href="">#4015</a>](<a href="">pgjdbc/pgjdbc#4015</a>)</li>
<li>fix: the read buffer returns to its initial size once the message that grew it is drained, so a connection no longer retains 32 MiB after one large error [Issue <a href="">#4015</a>](<a href="">pgjdbc/pgjdbc#4015</a>)</li>
<li>fix: exceeding <code>maxResultBuffer</code> closes the connection. The row is not read past the limit, so the connection cannot continue, and it is now dropped where the limit is exceeded rather than refused as a protocol violation at the next message. The error reported is the limit alone, with SQLState <code>08S01</code> as before [Issue <a href="">#4015</a>](<a href="">pgjdbc/pgjdbc#4015</a>)</li>
</ul>
<h3>Security</h3>
<ul>
<li>fix: a <code>requireAuth</code> value that excludes every authentication method, such as <code>!password,!md5,!gss,!sspi,!scram-sha-256,!none</code>, now refuses every method. A connection with such a value now fails with SQLState <code>08004</code>. Before, the driver treated the value as if <code>requireAuth</code> were not set, and used any method the server asked for, even a cleartext password. This affects 42.7.11 through 42.7.13 <a href="https://github.com/pgjdbc/pgjdbc/security/advisories/GHSA-rhp9-mr79-r74h">GHSA-rhp9-mr79-r74h</a></li>
<li>fix: a <code>requireAuth</code> value without a method in it, such as <code>,</code> or <code>,,</code>, now fails with SQLState <code>22023</code>. Before, the driver treated it as if <code>requireAuth</code> were not set. Commas at the very end of a value are still ignored, as in <code>password,</code>. This affects 42.7.11 through 42.7.13 <a href="https://github.com/pgjdbc/pgjdbc/security/advisories/GHSA-rhp9-mr79-r74h">GHSA-rhp9-mr79-r74h</a></li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>ebdd9d0</code></a> chore: bump version to 42.7.14</li>
<li><a href=""><code>0e764c8</code></a> test: Add additional PgBufferedOutputStream.writeZeros(...) tests</li>
<li><a href=""><code>c8998c8</code></a> fix: writeZeros() could send stale buffer contents instead of zeros</li>
<li><a href=""><code>a65ef98</code></a> fix: refuse every method when requireAuth excludes them all</li>
<li>See full diff in <a href="https://github.com/pgjdbc/pgjdbc/compare/REL42.7.13...REL42.7.14">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.postgresql:postgresql&package-manager=maven&previous-version=42.7.13&new-version=42.7.14)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d455beb296f8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.