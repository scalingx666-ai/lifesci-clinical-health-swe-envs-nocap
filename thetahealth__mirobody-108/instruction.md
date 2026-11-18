# Issue

**Title:** docker: purge the stub build so the image imports

## Description

`thetahealth4mirobody/mirobody:1.5.3` ships a **22-byte** `mirobody/__init__.py`.
`import mirobody` works; `mirobody.resolve` raises `ImportError`,
`mirobody.BUNDLE_VERSION` raises `AttributeError`, and the stdio MCP
`resources/read mirobody://bundle` returns an Internal error. The 1.5.3 wheel on
PyPI and the sdist are both correct, so this is the image only.

## Cause

The Dockerfile installs the project twice. The first install runs against a
one-line `mirobody/__init__.py` (line 25) so the `[app]` extra resolves before
the source is copied. setuptools leaves that build in `build/lib`, and its copy
step skips any file whose destination is not older than the source
(`distutils.file_util.copy_file`). The `COPY mirobody/ mirobody/` brings the real
tree with the checkout's mtimes, which are older than the `build/lib` copies
written moments earlier, so `mirobody/__init__.py` is the one file the second
build does not refresh. The 15 MB wheel that results carries every real module
except that one.

## Verification

Reproduced against this repo's own `scripts/build_backend.py`, pip 24.0 (the
image's pip), an in-tree build, and COPY-faithful mtimes:

| | installed `mirobody/__init__.py` |
| --- | --- |
| without the purge | **22 bytes** (the bug) |
| with `rm -rf build *.egg-info` | **3648 bytes** (the fix) |

pip 26 builds in an isolated temporary copy, which is why a normal local venv
never reproduces it. The fix is one line and cannot regress anything: nothing
after it reads `build/`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `49aa6d31281e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.