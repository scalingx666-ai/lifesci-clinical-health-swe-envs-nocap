# Issue

**Title:** (Docs) Add Guide for Deploying Application Config Across Environments

## Description

Implementers have documentation for individual resource operations and Bot deployment, but need a repeatable workflow for deploying application configuration across environments. This guide connects source control, resource identity, dependency ordering, verification, activation, and recovery using staging and production projects.

- Defines application configuration versions separately from Medplum server releases and notes that paid hosted plans include staging and production environments.
- Adds a runnable intake example with preview/apply commands, target-project checks, conditional creation, conflict detection, and preservation of published definitions.
- Covers forms, profiles, terminology, policies, plans, and subscriptions, with a short section for separate Medplum instances and shared reference projects.
- Includes two Mermaid diagrams, verification and recovery tables, and navigation links from Projects and Bots in Production.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b1e7dd6acd41`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.