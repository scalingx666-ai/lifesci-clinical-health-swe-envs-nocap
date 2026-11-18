# Issue

**Title:** maven(deps): bump org.mariadb.jdbc:mariadb-java-client from 3.5.9 to 3.5.10

## Description

Bumps [org.mariadb.jdbc:mariadb-java-client](https://github.com/mariadb-corporation/mariadb-connector-j) from 3.5.9 to 3.5.10.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/mariadb-corporation/mariadb-connector-j/releases">org.mariadb.jdbc:mariadb-java-client's releases</a>.</em></p>
<blockquote>
<h2>MariaDB Connector/Java 3.5.10</h2>
<h2><a href="https://github.com/mariadb-corporation/mariadb-connector-j/tree/3.5.10">3.5.10</a> (Jul 2026)</h2>
<p><a href="https://github.com/mariadb-corporation/mariadb-connector-j/compare/3.5.9...3.5.10">Full Changelog</a></p>
<h4>Key Enhancements</h4>
<ul>
<li>CONJ-1333 - Add maxAllowedPacket connection option (send/receive limit)</li>
<li>CONJ-1339 - Add maxAllowedColumns option to bound server-announced column count (report by fg0x0)</li>
<li>CONJ-1330 - add infer test to CI</li>
</ul>
<h4>Issues Resolved</h4>
<ul>
<li>CONJ-1332 - Reject multipart (&gt;16 MB) packets before authentication to prevent pre-auth OOM from a rogue server</li>
<li>CONJ-1342 - socketFactory option allows loading arbitrary bytecode via jar: URL, enabling RCE when JDBC URL is
attacker-controlled (report by Qing Xu)</li>
<li>CONJ-1307 - Connection.setReadOnly(true) still allows DML statements to execute</li>
<li>CONJ-1326 - Unsafe escaping in enquoteLiteral()/enquoteNCharLiteral() (thanks to jmestwa-coder)</li>
<li>CONJ-1327 - Align SSL hostname verification with TLS libraries (thanks to jmestwa-coder)</li>
<li>CONJ-1329 - LOAD DATA LOCAL INFILE validation fails open when a bound parameter can't be rendered (thanks to
jmestwa-coder)</li>
<li>CONJ-1331 - trustStore-configured TLS connections defer certificate-chain/identity validation instead of validating
up front (thanks to jmestwa-coder)</li>
<li>CONJ-1340 - SQL injection via unescaped identifiers in updatable ResultSet generated statements (thanks to
jmestwa-coder)</li>
<li>CONJ-1341 - MariaDbPoolDataSource.getConnection(user, password) ignores the user argument when the pool's own
password is supplied (report by fg0x0)</li>
<li>CONJ-1328 - restrictedAuth allowlist is matched with substring contains() instead of equality (thanks to
jmestwa-coder)</li>
<li>CONJ-1338 - Validate length-encoded integers fit a non-negative int before use as a length (report by fg0x0)</li>
<li>CONJ-1336 - CONJ-1282 regression: TLS connection fails when JDBC hostname is an absolute FQDN ending with a trailing
dot (report by Shaswata, thanks to Pepo48 for PR)</li>
<li>CONJ-1335 - getGeneratedKeys() throws &quot;integer overflow&quot; after a batch insert when the auto-increment value exceeds
Integer.MAX_VALUE, and returns bulk generated keys out of batch order</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/mariadb-corporation/mariadb-connector-j/blob/main/CHANGELOG.md">org.mariadb.jdbc:mariadb-java-client's changelog</a>.</em></p>
<blockquote>
<h2><a href="https://github.com/mariadb-corporation/mariadb-connector-j/tree/3.5.10">3.5.10</a> (Jul 2026)</h2>
<p><a href="https://github.com/mariadb-corporation/mariadb-connector-j/compare/3.5.9...3.5.10">Full Changelog</a></p>
<h4>Key Enhancements</h4>
<ul>
<li>CONJ-1333 - Add maxAllowedPacket connection option (send/receive limit)</li>
<li>CONJ-1339 - Add maxAllowedColumns option to bound server-announced column count (report by fg0x0)</li>
<li>CONJ-1330 - add infer test to CI</li>
</ul>
<h4>Issues Resolved</h4>
<ul>
<li>CONJ-1332 - Reject multipart (&gt;16 MB) packets before authentication to prevent pre-auth OOM from a rogue server</li>
<li>CONJ-1342 - socketFactory option allows loading arbitrary bytecode via jar: URL, enabling RCE when JDBC URL is
attacker-controlled (report by Qing Xu)</li>
<li>CONJ-1307 - Connection.setReadOnly(true) still allows DML statements to execute</li>
<li>CONJ-1326 - Unsafe escaping in enquoteLiteral()/enquoteNCharLiteral() (thanks to jmestwa-coder)</li>
<li>CONJ-1327 - Align SSL hostname verification with TLS libraries (thanks to jmestwa-coder)</li>
<li>CONJ-1329 - LOAD DATA LOCAL INFILE validation fails open when a bound parameter can't be rendered (thanks to
jmestwa-coder)</li>
<li>CONJ-1331 - trustStore-configured TLS connections defer certificate-chain/identity validation instead of validating
up front (thanks to jmestwa-coder)</li>
<li>CONJ-1340 - SQL injection via unescaped identifiers in updatable ResultSet generated statements (thanks to
jmestwa-coder)</li>
<li>CONJ-1341 - MariaDbPoolDataSource.getConnection(user, password) ignores the user argument when the pool's own
password is supplied (report by fg0x0)</li>
<li>CONJ-1328 - restrictedAuth allowlist is matched with substring contains() instead of equality (thanks to
jmestwa-coder)</li>
<li>CONJ-1338 - Validate length-encoded integers fit a non-negative int before use as a length (report by fg0x0)</li>
<li>CONJ-1336 - CONJ-1282 regression: TLS connection fails when JDBC hostname is an absolute FQDN ending with a trailing
dot (report by Shaswata, thanks to Pepo48 for PR)</li>
<li>CONJ-1335 - getGeneratedKeys() throws &quot;integer overflow&quot; after a batch insert when the auto-increment value exceeds
Integer.MAX_VALUE, and returns bulk generated keys out of batch order</li>
</ul>
<h2><a href="https://github.com/mariadb-corporation/mariadb-connector-j/tree/3.4.4">3.4.4</a> (Jul 2026)</h2>
<p><a href="https://github.com/mariadb-corporation/mariadb-connector-j/compare/3.4.3...3.4.4">Full Changelog</a></p>
<h5>Notable Changes</h5>
<ul>
<li>CONJ-1339 - Add maxAllowedColumns option to bound server-announced column count (report by fg0x0)</li>
</ul>
<h5>Bugs Fixed</h5>
<ul>
<li>CONJ-1332 - Reject multipart (&gt;16 MB) packets before authentication to prevent pre-auth OOM from a rogue server</li>
<li>CONJ-1342 - socketFactory option allows loading arbitrary bytecode via jar: URL, enabling RCE when JDBC URL is
attacker-controlled (report by Qing Xu)</li>
<li>CONJ-1326 - Unsafe escaping in enquoteLiteral()/enquoteNCharLiteral() (thanks to jmestwa-coder)</li>
<li>CONJ-1329 - LOAD DATA LOCAL INFILE validation fails open when a bound parameter can't be rendered (thanks to
jmestwa-coder)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>6164678</code></a> [misc] update changelog</li>
<li><a href=""><code>6f58858</code></a> [CONJ-1335] getGeneratedKeys() throws SQLDataException &quot;integer overflow&quot; aft...</li>
<li><a href=""><code>9f06db7</code></a> [misc] CI stability improvement</li>
<li><a href=""><code>99aa9e2</code></a> [CONJ-1336] correction follow up</li>
<li><a href=""><code>28a1550</code></a> [CONJ-1336] strip trailing dot from hostname before SNI and hostname verifica...</li>
<li><a href=""><code>b2b3f1b</code></a> [misc] limit authentication switch requests to 10 per connection</li>
<li><a href=""><code>26ca60a</code></a> [misc] bound the whole connection phase by connectTimeout</li>
<li><a href=""><code>15e08ff</code></a> [CONJ-1337] Limit parsec authentication PBKDF2 iteration factor to the connec...</li>
<li><a href=""><code>d3c4a72</code></a> bump 3.5.10 version</li>
<li><a href=""><code>d85e05f</code></a> [CONJ-1342] socketFactory option allows loading arbitrary bytecode via jar: U...</li>
<li>Additional commits viewable in <a href="https://github.com/mariadb-corporation/mariadb-connector-j/compare/3.5.9...3.5.10">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.mariadb.jdbc:mariadb-java-client&package-manager=maven&previous-version=3.5.9&new-version=3.5.10)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e3331f69a987`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.