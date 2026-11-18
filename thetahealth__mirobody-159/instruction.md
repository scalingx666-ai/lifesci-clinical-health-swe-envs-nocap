# Issue

**Title:** plugins: keep package context for path-configured dirs

## Description

Configuring an importable plugin directory by an absolute path, `..`, a trailing slash or a symlink could remove its package context. Modules with relative imports were skipped; for the built-in tools this dropped 4 of 9 tools, including `query_health_indicators`, when the server ran outside the checkout. The same resolver serves tool, agent and task discovery.

The resolver now finds package names from directory ancestry and existing import roots, retaining both logical and physical paths. It checks that an imported package points to the requested real directory before using its name. Symlinked parent packages and symlinked import roots retain their relative imports without modifying `sys.path`.

For a checkout beside a non-editable install, the documented package-relative spelling, such as `mirobody/agent/tools`, continues to reach the installed copy with a warning naming both locations. This also works for a regular package below a namespace parent without `__init__.py`. An explicit path that names no importable package keeps its own files, and a plain directory is never replaced by an installed namesake.

The two diagnostic warnings use the existing `# phi: ok <reason>` mechanism for deployment plugin paths and import names. The PHI baseline is unchanged. CHANGELOG, tool-discovery documentation and the testing guide describe the resulting behavior.

Validation:

- The shipped `test_plugin_dir_regressions.py` now has 21 library-only cases, including symlinked packages/import roots, namespace parents, installed-copy selection and plain-directory priority. Ten cases failed on the previous PR head and pass with the fix.
- Both independent review probes now register the synthetic tool; each previously registered zero tools on the PR head.
- Full local `pytest -q`: 641 passed, 105 skipped, 12 xfailed. No local test database was configured.
- Ruff (`mirobody examples benchmarks/windows`), compileall, import-linter (6 kept, 0 broken), bare-interpreter library imports, PHI lint, comment-style and version gates pass.
- Genomics benchmark suite: 37 tests, 2 skipped; health-records benchmark suite: 3 tests, passing.
- [GitHub CI run 39559187232](https://github.com/thetahealth/mirobody/actions/runs/39559187232) passed all seven checks on commit `73803607`: Python 3.12/3.13 test/build jobs (including minimal installs, PostgreSQL 17 and PHI gates), the Windows benchmark, Linux/macOS/Windows wheel-import checks and the summary job.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `74b931de9be6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.