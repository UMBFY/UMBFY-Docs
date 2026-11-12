# Sorting and Filtering

**What it does.** Gives the Media library the sort fields and filters it needs to be usable at scale, server-side
and paged.

**Where to find it.** The Media Order toolbar in **Media → Browse** for sorting and search; **Media → Collections**
for the advanced filters.

**Required permissions.** Media section access.

## Sort fields

| Field | Notes |
| --- | --- |
| Name | Alphabetical |
| Upload date | **The default**, descending |
| Last modified | |
| File size | |
| Width / Height | Needs a warm metadata index |
| Resolution | Needs a warm metadata index |
| Extension | |
| Media type | |
| Manual | Your own order |

Changing the sort **resets paging to the first page**, so you are never left looking at page 7 of a different
ordering.

### Default: upload date descending

A fresh upload appears at the top. After an upload the listing returns to upload-date descending, rather than
leaving the new file hidden somewhere inside whatever sort was active. Configurable with `DefaultSortField` and
`DefaultSortDirection` — see [Configuration](configuration.md#sorting).

### Remembered preference

Each editor's chosen sort is remembered in namespaced local storage, and per folder if
`FolderPreferencesEnabled` is on. Set `RememberUserChoice` to `false` for one consistent behaviour across the team.

## Filters

Filtering is a **server-side query with pagination**, not a client-side filter over the current page. You can filter
by:

- media type and extension
- size range
- date range
- dimension ranges and aspect ratio
- duplicates
- missing metadata
- favourites

!!! important "Advanced filters run in Collections"
    Browse is Umbraco's native list with the Media Order toolbar on top. The advanced filter surface lives in
    **Collections**. Build a filter in Browse and use **Apply in Collections** to carry it over.
    
    If a filter in Browse appears to do nothing, this is why — not a bug.

## Step-by-step: find your large images

1. Open **Media → Collections**.
2. Filter by media type *image*.
3. Add a size range filter — over 2&nbsp;MB, say.
4. Sort by file size descending.
5. Save the search if you will want it again. Saved searches are per user.

## Understanding the result

**A list rather than a blank page while the index warms up.** Advanced sorts that need the metadata index fall back
safely until it is ready. You get usable results, not an empty collection, and the ordering sharpens as indexing
completes. Check progress in [Insights](insights.md).

**Fewer results than expected.** Either a filter is narrower than you think, or you are a user with a restricted
media start node — in which case you are seeing your own folders, and totals are labelled as scoped. See
[Permissions](permissions.md).

## Limitations

- Width, height and resolution sorting depend on the metadata index. With `MetadataIndexingEnabled` off, they are
  not available.
- `MaxPageSize` bounds a page of results. Default 100, ceiling 200.
- Sorting applies to the native Umbraco media collection. Media Order adds to it rather than replacing it.

## Troubleshooting

| Symptom | Cause |
| --- | --- |
| Advanced filters seem to do nothing in Browse | They apply in Collections — use **Apply in Collections** |
| Dimension or resolution sort unavailable | The metadata index is still warming, or indexing is disabled |
| Ordering looks approximate right after install | The index is still warming; sorts fall back safely until it is ready |

See [Troubleshooting](troubleshooting.md).

## Related features

- [Collections](collections.md)
- [Insights](insights.md)
- [Configuration](configuration.md#sorting)
