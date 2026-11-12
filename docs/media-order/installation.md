# Media Order Installation

## Requirements

| | |
| --- | --- |
| NuGet package | `UMBFY.Umbraco.MediaOrder` |
| Version | 2.0 |
| Umbraco | 17.x and 18.x (`[17.0.0,19.0.0)`) |
| Database | SQL Server or SQLite. **SQL Server for large folder imports** |
| Backoffice assets | `/App_Plugins/UMBFY.MediaOrder/` |
| Options section | `UMBFY:MediaOrder` |
| Node.js | Not required |

Installing Media Order also installs [Hub](../hub/README.md). [Content Guard](../content-guard/README.md) is
**optional** — see [below](#content-guard-is-optional).

## 1. Install the package

```bash
dotnet add package UMBFY.Umbraco.MediaOrder
```

## 2. Restart so the migration runs

```bash
dotnet run
```

The migration creates the `umbfyMediaOrder*` tables on both SQL Server and SQLite. Let the site finish starting.

## 3. Let the metadata index warm up

Existing media is indexed **in the background** after install: file sizes, dimensions, and a SHA-256 fingerprint
for duplicate detection.

!!! tip "Hashing happens off the request path"
    Browsing is never blocked by it. You can use the library while the index builds.

While it warms up:

- advanced sorts **fall back safely** — you get a list, not a blank collection
- **Insights** totals climb as items are read

Watch the progress in **Media → Insights**. On a large library this takes a while; that is normal.

## 4. Find the three views

Open **Media**:

| Where | What |
| --- | --- |
| **Browse** | The native library plus the Media Order toolbar |
| **Collections** | Smart collections, saved searches, bulk actions. **Advanced filters run here** |
| **Insights** | Index health, rebuild, totals, CSV export |

Also on context menus: **Replace file…** on a media item, **Import folder…** on the Media root or a folder.

## 5. Verify the installation

1. Open **Media → Insights** and confirm the index is reporting and the totals are climbing or settled.
2. Open **Media → Browse** and confirm the toolbar appears above the native list.
3. Change the sort and confirm the list reorders, and that paging resets to the first page.
4. Open **Media → Collections** and open a smart collection — *recently uploaded* is the easiest to recognise.
5. Upload a file and confirm it appears at the top of Browse — default sort is Upload Date descending.

## 6. Optional: add the Smart Media Picker

To let editors upload from inside the content editor, add the **UMBFY Smart Media Picker** data type
(**Settings → Data Types**) to a property.

It stores native Media Picker values, so you can adopt and abandon it without migrating data. See
[Smart Media Picker](smart-media-picker.md).

## Content Guard is optional

With [Content Guard](../content-guard/README.md) installed, Media Order can answer "which media is potentially
unused?". Without it, that one query returns **empty rather than inventing usage**; everything else works
identically.

`ContentGuardIntegrationEnabled` (default `true`) controls the adapter. It is a soft integration — there is no hard
dependency.

## Upgrading from 0.x or 1.x

1. Update the package to `2.0.0`.
2. **Restart** so the migrations create the `umbfyMediaOrder*` tables.
3. Existing sort preferences in local storage keep working for `name`, `createDate` and `umbracoBytes`.
4. New feature flags default to **enabled**; disable individually if you want a narrower rollout.
5. Metadata hashing runs asynchronously after save and move. Browsing does not block on it.

### Behavioural changes to know about

- `MaxPageSize`'s upper bound is now **200** (it was 100). The default is still 100.
- The additional sort fields may need a warm metadata index. Until indexed, the list view falls back safely rather
  than showing a blank collection.
- Insights totals are **logical indexed sizes**, not guaranteed physical disk usage.

See [Versioning](../shared/versioning.md).

## Uninstalling

```bash
dotnet remove package UMBFY.Umbraco.MediaOrder
```

Your media is ordinary Umbraco media and is untouched — including anything created by a folder import, and
anything selected through the Smart Media Picker, which stored native Media Picker values all along.

If a property uses the Smart Media Picker, switch it back to the stock Media Picker. No data migration is needed.

## Next

- [Quick Start](quick-start.md)
- [Configuration](configuration.md)
- [Permissions](permissions.md)
