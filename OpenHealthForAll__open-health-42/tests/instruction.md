# Issue

**Title:** Optimize and make Container image rootless

## Description

## What's changed?
I've re-arranged and optimized the Containerfile inorder for it to properly use caching, so that only the images are rebuild of which there files have changed. So we don't build the dependencies everytime but instead only copy the files first that collects all the dependencies, build deps, cache this all and then we copy the source code and compile which changes more often.

Also made it rootless but i haven't tested this out yet.

Regarding this all, i've noticed a few things i would like to ask your opinion of:

- Would you be ok to change Dockerfile to Containterfile and favor using podman more of docker? Because it's more conform of the OCI standards aswell as being rootless by default (generally also more liked by the community).
- Instead of docker-compose, that we make it container-compose
- Instead of using postgresql that we use the alpine variant that's a bit smaller?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2196b0e4aaec`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.