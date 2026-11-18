# Issue

**Title:** Upgrade TemplateManagement to SharpCompress 0.48.0 and align stream reader usage

## Description

This updates TemplateManagement to SharpCompress 0.48.0 and applies the required StreamUtility API adjustment for compatibility with the newer SharpCompress reader surface. It also adds targeted unit coverage for decompression path behavior.

- **Dependency upgrade**
  - Updated `SharpCompress` in `Microsoft.Health.Fhir.TemplateManagement.csproj`:
    - `0.29.0` → `0.48.0`

- **StreamUtility compatibility update**
  - Updated tar.gz decompression reader creation in `StreamUtility`:
    - `ReaderFactory.Open(...)` → `ReaderFactory.OpenReader(...)`
  - No behavior change intended beyond API alignment for the upgraded package.

- **Unit test updates**
  - Added a focused test in `StreamUtilityTests` to verify `artifactFolder` prefix behavior during tar.gz decompression:
    - `GivenACompressedTarGzFile_WhenDecompressWithArtifactFolder_ArtifactNamesShouldContainFolderPrefix`

```csharp
// StreamUtility.cs
using var reader = ReaderFactory.OpenReader(tarGzStream);
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2ca6bcf855d7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.