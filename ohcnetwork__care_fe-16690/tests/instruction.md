# Issue

**Title:** refactor: remove obsolete PubSub from CARE

## Description

## Proposed Changes

- remove the obsolete PubSub context and provider from CARE
- remove the `PubSubProvider` wrapper from `App`
- remove the remaining `publish()` usage from public patient registration
- drop the unused subscribe/unsubscribe/publish event-bus code from core CARE

## Context

The old ABDM use case that needed PubSub has moved to a plugin and now uses `mutationKey` detection instead, so keeping PubSub in CARE core is no longer necessary.

## Testing

- verified the current in-repo PubSub references were limited to the PubSub module, the app provider wrapper, and the patient registration publish call
- removed those references as part of this cleanup
- CI checks pending on the updated branch

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [x] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Refactor**
  * Simplified application setup by removing the internal pub/sub layer.
  * Reorganized notification and update components without changing their visible settings or behavior.

* **Bug Fixes**
  * Patient registration continues directly to appointment creation after success.
  * Patient lists remain refreshed after registration, without triggering an unnecessary background event.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `37a3959b5dd1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.