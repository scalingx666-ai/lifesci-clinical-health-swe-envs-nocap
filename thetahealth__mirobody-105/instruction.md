# Issue

**Title:** docker: publish as thetahealth4mirobody/mirobody

## Description

Docker Hub's `thetahealth` belongs to an unrelated account (a Johannesburg health shop), so the `thetahealth/mirobody:1.5.3` that README and compose.yaml point at could never be published. This branch moves the image to `thetahealth4mirobody/mirobody`.

- `compose.yaml`, both READMEs: new image name.
- `docker-hub.yml`: the image name is one job-level `IMAGE`, and checkout uses the tag being published. Before this, a `workflow_dispatch` built whatever ref it ran on and labelled it with the input tag.

Credentials: repository variable `DOCKERHUB_USERNAME` and secret `DOCKERHUB_TOKEN` are set.

Verified: actionlint clean; `docker compose config --images` shows the new name; local README/deploy/config tests 99 passed (`test_deploy_script.py` updated locally). The 1.5.3 image is being published by dispatching this branch's workflow with `tag=1.5.3`; result in the comments.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c1aae297b4f3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.