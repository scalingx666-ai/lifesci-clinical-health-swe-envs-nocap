# Issue

**Title:** Gl 8648 fix expunge contained resources

## Description

## Summary

This PR fixes a `HAPI-2415` constraint violation that occurs when calling per-resource `$expunge` on a resource that is the TARGET of an `HFJ_RES_LINK` row owned by a still-alive resource. The failure surfaces specifically when `index_contained_resources=true` (with recursive indexing enabled), because the contained-resource indexer creates cross-resource link rows where the parent resource is the SOURCE and a referenced real resource is the TARGET — leaving an orphaned FK reference that blocked expunge.

The root cause was asymmetric cleanup: `JpaResourceExpungeService.deleteAllSearchParams` deleted SOURCE-side link rows (where the expunged resource is the source) but never deleted TARGET-side rows (where the expunged resource is the target). `ExpungeEverythingService` already performed symmetric cleanup on the bulk path; this PR brings the per-resource path into alignment.

Key changes:

1. **New DAO method** — `IResourceLinkDao.deleteByTargetResourceId(JpaPid)` issues a `DELETE FROM HFJ_RES_LINK WHERE TARGET_RESOURCE_ID = ?` to remove inbound link rows before the resource row itself is deleted.
2. **Service call** — `JpaResourceExpungeService.deleteAllSearchParams` now calls the new method at the end of its cleanup sequence, symmetrically matching the existing source-side deletion.
3. **Regression tests** — `ExpungeContainedResourcesR4Test` covers the primary failure scenario plus two adjacent cases (expunge-everything and expunge on a non-contained-indexed resource).
4. **Changelog** — `8648-fix-expunge-contained-resources.yaml` recorded under `8_12_0` (`type: fix`).

---

## Code Review Suggestions

- [ ] **`isHasLinks()` flag is SOURCE-side only.** `ResourceTable.isHasLinks()` describes whether the resource has outbound link rows (SOURCE). There is no symmetric `isTargetOfLinks()` flag, so the new `deleteByTargetResourceId` call is intentionally unconditional — it always runs a single indexed lookup. Reviewers should confirm this is acceptable rather than expecting a guard flag.
- [ ] **Alive-source side-effect.** When a resource is expunged, any `HFJ_RES_LINK` rows where it is the TARGET (but whose SOURCE is still alive) will be deleted. The source resource's serialized JSON blob is unaffected; only the index row is removed. This matches `ExpungeEverythingService` behaviour — but reviewers should confirm no secondary index or search query relies on TARGET-side link rows for a live source resource remaining present after its target is expunged.
- [ ] **FK symmetry with `ResourceTableFKProvider`.** The change aligns cleanup with `ResourceTableFKProvider#getResourceForeignKeys` (lines 59–60), which already enumerates both `SRC_RESOURCE_ID` and `TARGET_RESOURCE_ID` columns. Confirm the ordering of deletions in `deleteAllSearchParams` is consistent with FK dependency order.
- [ ] **Performance — unconditional DELETE on every soft-delete path.** The new `DELETE FROM HFJ_RES_LINK WHERE TARGET_RESOURCE_ID = ?` executes on every `BaseHapiFhirDao#updateResource` call where `newParams == null` — which covers every soft-delete and every save under `RESOURCE_SKIP_INDEXING`. For resources with no inbound links this is a single indexed lookup returning zero rows: cheap but not free. On high-write deployments or tables with heavy link traffic this adds a round-trip per delete. **Persistence-team reviewers should assess whether this is acceptable or whether a pre-check (e.g. a count query or a flag) would be warranted.**
- [ ] **Test scope.** The reproduction test uses `index_contained_resources=true` with recursive indexing. Verify the test storage-settings setup accurately reflects how this feature is typically deployed.

---

## Test Plan / QA Suggestions

### Setup
- [ ] Deploy a HAPI-FHIR JPA server (R4) with `daoConfig.setIndexContainedResources(IndexEnabledEnum.ENABLED)` and recursive contained indexing enabled.

### Integration test scenarios

- [ ] **Primary scenario — expunge of a cross-resource link target:** Create a parent resource (e.g. `Organization`) containing an inline `Practitioner`. Have that contained practitioner reference a standalone `Patient`. Verify the contained-resource indexer writes an `HFJ_RES_LINK` row from the `Organization` (SOURCE) to the `Patient` (TARGET). Delete the `Patient`. Call `$expunge` with `expungeDeletedResources=true` on the `Patient`. **Pre-fix:** fails with `HAPI-2415`. **Post-fix:** succeeds; confirm the `HFJ_RES_LINK` row pointing at the expunged `Patient` is gone.
- [ ] **Expunge-everything path still works:** Run `$expunge` with `expungeEverything=true` on a server containing contained-resource link rows. Confirm no constraint violations and all `HFJ_RES_LINK` rows are cleared.
- [ ] **Non-contained-indexed resource:** Expunge a resource that has never been the target of a contained-resource link row. Confirm the new `deleteByTargetResourceId` call completes without error (zero-row delete).
- [ ] **Live-source resource unaffected:** After expunging the TARGET resource, fetch the SOURCE resource (the one that contained the reference). Confirm it is still readable and its FHIR representation is unchanged — only the index row was removed.
- [ ] **Regression — standard expunge unaffected:** Verify existing expunge behaviour (resources with no inbound links) is unchanged in performance and correctness.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bc9575abee97`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.