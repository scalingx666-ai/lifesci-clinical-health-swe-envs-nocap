# Issue

**Title:** Docker support for dicoogle

## Description

Simple Dockerfile to allow the creation of a docker image for dicoogle. 

The docker image is based in the latest ubuntu image and will allow both build and run of dicoogle from inside the container.
 - Build :   docker build -t bioinformatics-ua/dicoogle .
 - Run :    docker run -t bioinformatics-ua/dicoogle
 - Access container :    docker run -it bioinformatics-ua/dicoogle bash

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9d612ad883c4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.