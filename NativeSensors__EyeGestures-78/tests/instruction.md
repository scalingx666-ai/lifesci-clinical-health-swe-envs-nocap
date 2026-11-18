# Issue

**Title:** Add nix shell with direnv

## Description

Hello! Thanks for this awesome library. Here's some quick DX improvements for nix users (purely additive).

`shell.nix` makes it so that running `nix-shell` in the directory creates an ephemeral environment with all dependencies installed from the `<nixpkgs>` on your `NIX_PATH`.

`flake.nix` make it so that running `nix develop` in the directory does the same, but from a nixpkgs revision pinned in `flake.lock`.

Direnv makes it so that, after you `cp .envrc.template .envrc && direnv allow`, whenever you cd into the directory, you enter the aforementioned ephemeral shell (cached if using [nix-direnv](https://github.com/nix-community/nix-direnv)).

Let me know if you think the shell isn't minimal/complete!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `91fa8402c125`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.