# Media Order Configuration

All options live under `UMBFY:MediaOrder`. **Everything is optional and every feature flag defaults to on**, so a
working installation needs no configuration at all.

## Full example

```json
{
  "UMBFY": {
    "MediaOrder": {
      "DefaultSortField": "createDate",
      "DefaultSortDirection": "desc",
      "RememberUserChoice": true,
      "FolderPreferencesEnabled": true,
      "AdvancedFiltersEnabled": true,
      "FavoritesEnabled": true,
      "SmartCollectionsEnabled": true,
      "DuplicateDetectionEnabled": true,
      "MetadataIndexingEnabled": true,
      "InsightsEnabled": true,
      "ContentGuardIntegrationEnabled": true,
      "MaxPageSize": 100,
      "MaxBatchSize": 100,
      "HashingConcurrency": 2,
      "MaxIndexedFileSizeBytes": 104857600,
      "LargeFileThresholdBytes": 10485760,
      "IndexBatchSize": 50,
      "FolderImportEnabled": true,
      "MaxImportFiles": 1000,
      "MaxImportFolders": 250,
      "MaxImportDepth": 10,
      "ImportUploadConcurrency": 3
    }
  }
}
```

Environment-variable form uses the standard .NET double-underscore separator:

```bash
UMBFY__MediaOrder__FolderImportEnabled=false
```

## Sorting

| Setting | Default | Purpose |
| --- | --- | --- |
| `DefaultSortField` | `createDate` | The initial sort field |
| `DefaultSortDirection` | `desc` | The initial direction |
| `RememberUserChoice` | `true` | Persist each editor's chosen sort in namespaced local storage |
| `FolderPreferencesEnabled` | `true` | Remember preferences per folder |

The default of **upload date, descending** is deliberate: a fresh upload should appear at the top rather than being
buried wherever the editor's last sort happened to put it. Change it only if your team genuinely works
alphabetically.

Setting `RememberUserChoice` to `false` makes every editor start from the configured default every time — useful
when you want one consistent library behaviour across a team.

See [Sorting and Filtering](sorting.md).

## Feature flags

Each of these turns a whole feature off. All default to `true`.

| Setting | Turns off |
| --- | --- |
| `AdvancedFiltersEnabled` | The advanced filter surface in [Collections](collections.md) |
| `FavoritesEnabled` | Per-user [favourites](collections.md#favourites) |
| `SmartCollectionsEnabled` | The virtual [smart collections](collections.md) |
| `DuplicateDetectionEnabled` | [Duplicate](duplicates.md) grouping and the SHA-256 fingerprint |
| `MetadataIndexingEnabled` | The metadata index — and with it the advanced sorts that depend on it |
| `InsightsEnabled` | The [Insights](insights.md) view |
| `FolderImportEnabled` | [Folder import](upload-folders.md) |
| `ContentGuardIntegrationEnabled` | The optional [Content Guard](../content-guard/README.md) adapter |

!!! note "`MetadataIndexingEnabled` is the load-bearing one"
    Turning it off disables the index that the dimension, resolution and duplicate features read. The library still
    works and the basic sorts still work; the advanced ones fall back.

## Paging and batching

| Setting | Default | Purpose |
| --- | --- | --- |
| `MaxPageSize` | `100` | Upper bound on a page of results. The ceiling is **200** |
| `MaxBatchSize` | `100` | Upper bound on a [bulk operation](bulk-operations.md) |

`MaxPageSize`'s ceiling rose from 100 to 200 in 2.0. The default did not change.

## Indexing and hashing

| Setting | Default | Purpose |
| --- | --- | --- |
| `MetadataIndexingEnabled` | `true` | Whether the index is maintained |
| `HashingConcurrency` | `2` | How many files are hashed at once |
| `IndexBatchSize` | `50` | How many items are indexed per batch |
| `MaxIndexedFileSizeBytes` | `104857600` (100&nbsp;MB) | Files above this are not hashed |
| `LargeFileThresholdBytes` | `10485760` (10&nbsp;MB) | What counts as a "large file" in Insights |

Hashing is streaming SHA-256 and runs **off the request path**, so browsing never blocks on it. Raising
`HashingConcurrency` speeds the initial warm-up at the cost of I/O; on shared hosting, leave it alone.

`MaxIndexedFileSizeBytes` exists so that a handful of enormous video files cannot dominate the index. Files above it
are still ordinary media; they simply have no fingerprint, so they do not participate in duplicate detection.

`LargeFileThresholdBytes` is purely a reporting threshold — it changes what Insights calls large, nothing else.

## Folder import limits

| Setting | Default | Purpose |
| --- | --- | --- |
| `FolderImportEnabled` | `true` | Whether folder import is offered |
| `MaxImportFiles` | `1000` | Files per import |
| `MaxImportFolders` | `250` | Folders per import |
| `MaxImportDepth` | `10` | How deep a hierarchy may be |
| `ImportUploadConcurrency` | `3` | Parallel uploads during an import |

These are guard rails against somebody dragging a 40&nbsp;GB archive at a production site. Raise them deliberately,
and read the SQLite caveat in [Folder Import](upload-folders.md) first.

## Multi-server installations

Hashing coordination uses the package's own operation and index status rows, so a multi-server installation needs a
**shared database**. It does not need any extra configuration beyond that.

## Next

- [Sorting and Filtering](sorting.md)
- [Permissions](permissions.md)
- [Troubleshooting](troubleshooting.md)
