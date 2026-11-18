# Issue

**Title:** feat(cli): add openmed config provenance command

## Description

# Pull Request

## Description
Adds an `openmed config provenance` subcommand that prints the value-free precedence report from `audit_configuration()`, so "why is this setting what it is" can be answered from the CLI instead of requiring Python.

## Type of Change
- [ ] Bug fix (non-breaking change which fixes an issue)
- [x] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] Documentation update
- [ ] Code refactoring
- [ ] Performance improvement
- [x] Test addition/improvement

## Changes Made
- Register a `provenance` leaf under `openmed config` in `openmed/cli/main.py`; the parser finalizer attaches the uniform `--json` flag and `config provenance` command path automatically.
- The handler calls `audit_configuration()` with the resolved config file path when it exists (a missing file audits defaults + environment only, mirroring `config show` fallback behaviour) and an `os.environ` snapshot.
- Output goes through the existing `emit()` helper: `--json` emits the documented report shape (`schema_version`, `precedence`, per-key `source_class`/`conflict_category`/`sources`/`overridden_sources`); human mode prints one `key  source  conflict` line per key. Configuration values are never printed.
- Add `tests/unit/cli/test_config_provenance_cli.py` covering the JSON shape, environment winning over file for `device`, the human line format, the missing-file case, and that a planted `hf_token` value never appears in stdout or stderr.

## Testing
- [x] I have added tests that prove my fix is effective or that my feature works
- [x] New and existing unit tests pass locally with my changes
- [ ] I have tested this change with different models/inputs

Commands run:
- `.venv/bin/python -m pytest tests/unit/cli/test_config_provenance_cli.py -q` — 3 passed.
- `.venv/bin/python -m pytest tests/unit/core/test_config_provenance.py tests/unit/cli/test_cli_json_output.py -q` — 20 passed, 1 skipped.
- Manual smoke: `openmed config provenance --json` prints the report envelope with `command: "config provenance"`.

## Documentation
- [ ] I have updated the documentation accordingly
- [x] I have added docstrings to new functions/classes
- [ ] I have updated the CHANGELOG.md

The report format is already documented in `docs/configuration/precedence-audit.md`; this PR only adds the CLI surface for it.

## Code Quality
- [x] I ran `make format`, `make lint`, and `make format-check`
- [ ] For Swift/OpenMedKit changes, I ran `make format-swift` and `make lint-swift`
- [x] I have performed a self-review of my own code
- [x] I have commented my code, particularly in hard-to-understand areas
- [x] My changes generate no new warnings

Validated with the scoped equivalent, `pre-commit run --files openmed/cli/main.py tests/unit/cli/test_config_provenance_cli.py` — all hooks passed (ruff check, ruff format, bandit). No Swift files touched.

## Dependencies
- [x] I have not added any new dependencies
- [ ] OR I have added new dependencies and they are justified because: ____

## Checklist
- [x] I have read the [contributing guide](https://github.com/maziyarpanahi/openmed/blob/master/CONTRIBUTING.md), [Code of Conduct](https://github.com/maziyarpanahi/openmed/blob/master/CODE_OF_CONDUCT.md), and [maintainer guide](https://github.com/maziyarpanahi/openmed/blob/master/MAINTAINERS.md)
- [x] My commits have clear, descriptive messages
- [x] I have squashed/organized my commits appropriately

## Related Issues

## Screenshots/Examples
```text
$ openmed config provenance
backend  default  none
device  environment  overridden
hf_token  file  none
...
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b5bf9fc0c9c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.