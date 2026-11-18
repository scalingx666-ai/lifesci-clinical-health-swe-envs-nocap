# Issue

**Title:** github-actions(deps): bump actions/setup-java from 5.7.0 to 6.0.0

## Description

Bumps [actions/setup-java](https://github.com/actions/setup-java) from 5.7.0 to 6.0.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/setup-java/releases">actions/setup-java's releases</a>.</em></p>
<blockquote>
<h2>v6.0.0</h2>
<h2>What's Changed</h2>
<ul>
<li>dist: Migrate from Zulu Discovery API to Azul Metadata API by <a href="https://github.com/jameswald"><code>@​jameswald</code></a> in <a href="">actions/setup-java#1010</a></li>
<li>feat: add .mvn/extensions.xml to Maven cache key pattern by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> with <a href="https://github.com/Copilot"><code>@​Copilot</code></a> in <a href="">actions/setup-java#1041</a></li>
<li>Migrate to ESM and upgrade dependencies by <a href="https://github.com/priyagupta108"><code>@​priyagupta108</code></a> in <a href="">actions/setup-java#1078</a></li>
<li>Map Zulu x86 architecture to i686 for Azul Metadata API by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1079</a></li>
<li>Rename jdkFile input to jdk-file with deprecated alias by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1083</a></li>
<li>Infer distribution from asdf .tool-versions vendor prefix by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1084</a></li>
<li>Add Maven compiler problem matcher for javac diagnostics by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1086</a></li>
<li>feat: expose cache-primary-key output (<a href="">#597</a>) by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1088</a></li>
<li>docs: clarify V6 ESM migration is not a user-facing breaking change by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1090</a></li>
<li>Support multi-field Java versions like <code>18.0.1.1</code> by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1092</a></li>
<li>docs: document seeding the Maven cache for plugin dependencies by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1094</a></li>
<li>docs: clarify Maven cache paths and key hash inputs by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1096</a></li>
<li>Support pinning java-version as &quot;latest&quot; by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1093</a></li>
<li>chore(deps-dev): bump eslint from 10.6.0 to 10.7.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/setup-java#1101</a></li>
<li>chore(deps-dev): bump eslint-plugin-n from 18.2.1 to 18.2.2 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/setup-java#1103</a></li>
<li>chore(deps-dev): bump prettier from 3.9.4 to 3.9.5 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/setup-java#1105</a></li>
<li>chore(deps): bump actions/checkout from 6 to 7 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/setup-java#1106</a></li>
<li>chore(deps-dev): bump <code>@​types/node</code> from 26.1.0 to 26.1.1 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/setup-java#1104</a></li>
<li>dist: Cover Tencent Kona JDK 25 by <a href="https://github.com/johnshajiang"><code>@​johnshajiang</code></a> in <a href="">actions/setup-java#1108</a></li>
<li>chore(deps-dev): bump typescript from 6.0.3 to 7.0.2 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/setup-java#1102</a></li>
<li>Preserve Maven toolchains across repeated setup-java runs (<a href="">#1099</a>) by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1111</a></li>
<li>dist: Support Liberica NIK (<a href="">#878</a>) by <a href="https://github.com/asm0dey"><code>@​asm0dey</code></a> in <a href="">actions/setup-java#1112</a></li>
<li>Fix template injection (zizmor alert <a href="">#118</a>) in e2e-versions.yml by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> with <a href="https://github.com/Copilot"><code>@​Copilot</code></a> in <a href="">actions/setup-java#1114</a></li>
<li>Fix template injection in e2e-versions.yml (zizmor alert <a href="">#122</a>) by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> with <a href="https://github.com/Copilot"><code>@​Copilot</code></a> in <a href="">actions/setup-java#1120</a></li>
<li>Disable persisted checkout credentials in e2e workflow by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> with <a href="https://github.com/Copilot"><code>@​Copilot</code></a> in <a href="">actions/setup-java#1115</a></li>
<li>feat: Update recommended configuration for GPG signing by <a href="https://github.com/wetneb"><code>@​wetneb</code></a> in <a href="">actions/setup-java#608</a></li>
<li>Cache Maven and Gradle wrapper distributions separately from the dependency cache by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1097</a></li>
<li>Consolidate cache-dependency-path e2e workflow and add maven/sbt coverage by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1124</a></li>
<li>Use gpg.passphraseEnvName instead of the deprecated gpg.passphrase server by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1123</a></li>
<li>Extract repeated directory-check assertions into check-dir.sh helper by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1127</a></li>
<li>Consolidate duplicate jobs in e2e-versions workflow by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1125</a></li>
<li>Use YAML anchors to reduce boilerplate in e2e-versions workflow by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1126</a></li>
<li>Updated msft json for now by <a href="https://github.com/jmjaffe37"><code>@​jmjaffe37</code></a> in <a href="">actions/setup-java#1129</a></li>
<li>Document missing action inputs in README by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1130</a></li>
<li>chore(deps): bump <code>@​actions/cache</code> to 6.2.0 by <a href="https://github.com/philip-gai"><code>@​philip-gai</code></a> in <a href="">actions/setup-java#1128</a></li>
<li>Add an option to disable Java problem matchers by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1133</a></li>
<li>docs: update setup-java examples by <a href="https://github.com/HarithaVattikuti"><code>@​HarithaVattikuti</code></a> in <a href="">actions/setup-java#1131</a></li>
<li>Clarify credential environment variable inputs by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1134</a></li>
<li>chore(deps-dev): bump <code>@​typescript-eslint/eslint-plugin</code> from 8.63.0 to 8.64.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/setup-java#1135</a></li>
<li>chore(deps): bump actions/setup-python from 6 to 7 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/setup-java#1143</a></li>
<li>chore(deps): bump fast-xml-parser from 5.9.3 to 5.10.1 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/setup-java#1142</a></li>
<li>chore(deps-dev): bump <code>@​typescript-eslint/parser</code> from 8.64.0 to 8.65.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/setup-java#1138</a></li>
<li>chore(deps-dev): bump lint-staged from 17.0.8 to 17.2.0 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/setup-java#1136</a></li>
<li>chore(deps-dev): bump typescript from 6.0.3 to 7.0.2 by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">actions/setup-java#1137</a></li>
<li>chore(deps): fix npm audited vulnerabilities by <a href="https://github.com/mhoffrog"><code>@​mhoffrog</code></a> in <a href="">actions/setup-java#1140</a></li>
<li>Fix formatting issues in README.md by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> in <a href="">actions/setup-java#1144</a></li>
<li>Remediate npm audit findings and rebuild distributions by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> with <a href="https://github.com/Copilot"><code>@​Copilot</code></a> in <a href="">actions/setup-java#1145</a></li>
<li>Set GRAALVM_HOME for GraalVM distributions by <a href="https://github.com/brunoborges"><code>@​brunoborges</code></a> with <a href="https://github.com/Copilot"><code>@​Copilot</code></a> in <a href="">actions/setup-java#1146</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>dd06d9c</code></a> Prepare documentation for v6 release (<a href="">#1253</a>)</li>
<li><a href=""><code>59b3450</code></a> chore(deps): combine open Dependabot npm updates (<a href="">#1252</a>)</li>
<li><a href=""><code>b96213d</code></a> Set default signature verification for supported distributions (<a href="">#1246</a>)</li>
<li><a href=""><code>1dbac3c</code></a> docs: expose contributing guide to GitHub (<a href="">#1245</a>)</li>
<li><a href=""><code>11741d6</code></a> ci: constrain cache e2e job modes (<a href="">#1244</a>)</li>
<li><a href=""><code>ff99aa1</code></a> Fix Oracle macOS E2E version (<a href="">#1243</a>)</li>
<li><a href=""><code>416c6d1</code></a> Add Red Hat Build of OpenJDK support (<a href="">#1241</a>)</li>
<li><a href=""><code>5f75b27</code></a> Add Maven dependency-resolution repositories (<a href="">#1240</a>)</li>
<li><a href=""><code>a42a52c</code></a> Add multiple Maven server credentials (<a href="">#1239</a>)</li>
<li><a href=""><code>fb4abd7</code></a> test: cover JDK 26 from SDKMAN (<a href="">#1238</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/actions/setup-java/compare/v5.7.0...v6">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/setup-java&package-manager=github_actions&previous-version=5.7.0&new-version=6.0.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4793794c23e4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.