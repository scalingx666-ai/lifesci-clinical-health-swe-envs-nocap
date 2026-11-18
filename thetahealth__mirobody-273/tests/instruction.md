# Issue

**Title:** ci: build a Docker tag that is not PEP 440 as a local version

## Description

## Why

`docker-hub.yml` accepts any `X.Y.Z[.-suffix]` tag and also passes it to the build as the Python package's version. A test image for #272 dispatched as `1.6.0-fix.1` passed the tag check and then failed in `pip install` with `InvalidVersion: '1.6.0-fix.1'` ([run 42750484937](https://github.com/thetahealth/mirobody/actions/runs/42750484937)). `-rc1` only works because `rc` happens to be a PEP 440 segment.

## Change

The image keeps the tag it was asked for. The package inside gets a valid version: a suffix PEP 440 does not know becomes a local version, so `1.6.0-fix.1` builds `1.6.0+fix.1`. Every tag that already parses passes unchanged (`1.6.0`, `1.5.3-rc1`, `1.6.0.post1`), so release builds are unaffected.

## Checked

The step's script, run against the parsed YAML for those four tags. The `1.6.0-fix.1` image is being published by dispatching this branch's workflow with `source_ref` set to #272's head.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f5516978cff1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.