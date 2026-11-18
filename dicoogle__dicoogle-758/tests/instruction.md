# Issue

**Title:** fix: read empty archive list elements as empty lists instead of null

## Description

## Summary

Fixes a startup failure when Dicoogle is launched with an existing `confs/server.xml` containing empty `<dim-providers/>` or `<default-storages/>` elements.

## Problem

When no DIM providers or default storages are configured, for example, on a the first run of a fresh install, the lists are serialized as empty XML elements:

```xml
<dim-providers/>
<default-storages/>
```

On the next startup, Jackson deserializes these empty wrapped elements as `null` instead of an empty list. `WSICache` then calls `isEmpty()` directly:

```java
List<String> dicomProviders = ServerSettingsManager.getSettings()
        .getArchiveSettings()
        .getDIMProviders();
if (!dicomProviders.isEmpty()) { // NPE: dicomProviders is null
```

This aborts web server startup:

```text
java.lang.NullPointerException: Cannot invoke "java.util.List.isEmpty()"
because "dicomProviders" is null
    at pt.ua.dicoogle.server.web.utils.cache.WSICache.<init>(WSICache.java:58)
    ...
    at pt.ua.dicoogle.server.ControlServices.startWebServer(ControlServices.java:196)
```

## Fix

Add `@JsonSetter(nulls = Nulls.AS_EMPTY)` to the archive list getters in `ServerSettingsReader.Archive`:

- `getDIMProviders()`
- `getDefaultStorage()`

This makes Jackson deserialize null/empty wrapped XML elements as empty lists.

The change is deserialization-only. Existing `server.xml` files remain valid and are still written in the same format, so no migration is needed.

## Testing

1. Start Dicoogle with no `confs/server.xml` so a default configuration is generated.
2. Confirm the generated file contains `<dim-providers/>` and `<default-storages/>`.
3. Start Dicoogle again using that existing configuration.
4. Confirm the web server starts successfully and the web interface loads.
5. Optionally verify that `getDIMProviders()` and `getDefaultStorage()` return empty lists instead of `null`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1071b98f558e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.