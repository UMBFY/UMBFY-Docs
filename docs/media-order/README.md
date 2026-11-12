<section class="umbfy-product-hero">
  <span class="umbfy-product-hero__eyebrow">UMBFY PACKAGE · MEDIA PRODUCTIVITY</span>
  <h1>Media Order</h1>
  <p>Turns the native Umbraco Media library into something you can work in at scale: real sorting and filtering, smart collections, duplicate detection, bulk operations, folder upload, controlled file replacement and library insights.</p>
  <div class="umbfy-product-meta">
    <span>Umbraco 17</span>
    <span>Umbraco 18</span>
    <span>Version 2.0</span>
    <span>Native Media preserved</span>
  </div>
  <div class="umbfy-actions">
    <a class="umbfy-btn umbfy-btn--primary" href="installation/">Install Media Order</a>
    <a class="umbfy-btn umbfy-btn--ghost" href="quick-start/">Quick start</a>
  </div>
</section>

It **adds to** the Media section. It does not replace Umbraco's Media tree, its upload pipeline, or its permissions
model — and a media item created by Media Order is an ordinary Umbraco media item.

## Start here

<div class="umbfy-doc-grid">
  <a class="umbfy-doc-card" href="installation/">
    <strong>Installation</strong>
    <span>Install, migrate, and let the metadata index warm up.</span>
  </a>
  <a class="umbfy-doc-card" href="quick-start/">
    <strong>Quick Start</strong>
    <span>Find the three views, run a real filter, import a folder.</span>
  </a>
  <a class="umbfy-doc-card" href="configuration/">
    <strong>Configuration</strong>
    <span>All 21 options, their defaults, and which ones you would actually change.</span>
  </a>
  <a class="umbfy-doc-card" href="troubleshooting/">
    <strong>Troubleshooting</strong>
    <span>Filters that seem to do nothing, stalled imports, index that looks short.</span>
  </a>
</div>

## Browse, Collections and Insights

Media Order adds three places to the **Media** section, and knowing which does what saves the single most common
piece of confusion:

| Where | What |
| --- | --- |
| **Media → Browse** | Umbraco's own library, plus the Media Order toolbar: search, sort, filter chips, **Import folder** |
| **Media → Collections** | Smart collections, your saved searches, grid or table view, and bulk actions. **Advanced filters run here** |
| **Media → Insights** | Index health and **Rebuild index**, totals, type breakdown, largest files, duplicate groups, CSV export |

!!! tip "Browse vs Collections"
    Browse is Umbraco's native list with a toolbar on top. The **advanced filters apply in Collections**. If you
    build a filter in Browse, use **Apply in Collections** to carry it over. Knowing this up front saves a support
    ticket.

Two more entries live on context menus: **Replace file…** on a media item, and **Import folder…** on the Media root
or any folder.

## Core features

### Sorting and filtering

Sort by name, upload date, last modified, file size, width, height, resolution, extension, media type, or manually.
Filter server-side with pagination by type, extension, size, date, dimension ranges, aspect ratio, duplicates,
missing metadata and favourites.

Default sort stays **Upload Date descending**, so a fresh upload appears at the top rather than buried in whatever
sort you were last using.

[Read the Sorting and Filtering guide &rarr;](sorting.md)

### Collections and favourites

Virtual smart collections — recently uploaded, large files, duplicates, missing metadata, needs attention — plus
per-user saved searches and per-user favourites.

[Read the Collections guide &rarr;](collections.md)

### Duplicate detection

A streaming SHA-256 index groups byte-identical files. **Nothing is ever auto-deleted**; you get the groups and
decide.

[Read the Duplicates guide &rarr;](duplicates.md)

### Bulk operations

Rename with a preview before you commit, move, and add or remove favourites — with per-item authorization, so a
bulk action cannot do what the user could not do one at a time.

[Read the Bulk Operations guide &rarr;](bulk-operations.md)

### Folder import

Upload a whole folder with its hierarchy intact: conflict handling, a preview tree, live progress, cancel,
retry-failed and a CSV report. **Nothing is ever overwritten.**

[Read the Folder Import guide &rarr;](upload-folders.md)

### Replace file

Swap the file behind a media item while keeping the item — so every reference to it survives. URLs and crops can
still change, and the dialog says so before you commit.

[Read the Replace File guide &rarr;](replace-file.md)

### Smart Media Picker

A property editor that lets editors pick existing media, upload files, upload a folder or drag and drop — without
leaving the page they are editing. It stores **native Media Picker values**, so Razor, the Delivery API, crops and
focal points keep working, and you can swap back to the stock picker without migrating data.

[Read the Smart Media Picker guide &rarr;](smart-media-picker.md)

### Insights

Index health and rebuild, totals, type breakdown, largest files, missing metadata, duplicate groups and a CSV
report.

[Read the Insights guide &rarr;](insights.md)

## Content Guard integration is optional

With [Content Guard](../content-guard/README.md) installed, Media Order can answer "which media is potentially
unused?".

Without it, that query **returns empty rather than inventing usage**. The package works perfectly well on its own;
it simply does not guess at something it cannot know.

## Install

```bash
dotnet add package UMBFY.Umbraco.MediaOrder
```

No Node.js required. Restart so the migration can create its `umbfyMediaOrder*` tables — SQL Server and SQLite are
both supported. See [Installation](installation.md).

## Permissions

Everything requires **Media** section access. Editors restricted to a media start node see only their own folders,
and their totals are **labelled as scoped** rather than presented as site-wide. **Rebuild index** additionally
requires unrestricted media access, because it re-reads the whole library. CSV exports never include storage paths
and only contain items the user may see.

[Read the Permissions guide &rarr;](permissions.md)

## Known limitations

- It does not replace the native Media tree, upload pipeline or permissions model.
- **Advanced filters run in Collections**, not Browse.
- Large folder imports want **SQL Server**. On SQLite, Umbraco's own cache sync can stall under sustained media
  creation.
- Folder import resolves name conflicts **when it plans**. Items created by somebody else mid-import are not
  re-checked — though nothing is ever overwritten.
- Duplicate detection is **binary** (SHA-256). Perceptual similarity is an extension point only, not a feature.
- Insights totals are **logical indexed sizes**, not guaranteed physical disk usage.
- The Smart Media Picker uses a package modal override on the same alias. Preserve selection values and re-validate
  after an Umbraco upgrade.
- Multi-server hashing coordination relies on shared package rows, so it needs a **shared database**.

## Documentation map

<div class="umbfy-doc-grid">
  <a class="umbfy-doc-card" href="sorting/"><strong>Sorting and Filtering</strong><span>Every sort field and filter, and where each applies.</span></a>
  <a class="umbfy-doc-card" href="collections/"><strong>Collections</strong><span>Smart collections, saved searches and favourites.</span></a>
  <a class="umbfy-doc-card" href="duplicates/"><strong>Duplicates</strong><span>SHA-256 groups, and why nothing is deleted for you.</span></a>
  <a class="umbfy-doc-card" href="bulk-operations/"><strong>Bulk Operations</strong><span>Rename preview, move and favourites with per-item auth.</span></a>
  <a class="umbfy-doc-card" href="upload-folders/"><strong>Folder Import</strong><span>Whole-folder upload with conflict handling and a report.</span></a>
  <a class="umbfy-doc-card" href="replace-file/"><strong>Replace File</strong><span>Swap the file, keep the item and its references.</span></a>
  <a class="umbfy-doc-card" href="smart-media-picker/"><strong>Smart Media Picker</strong><span>Upload from the content editor, native values preserved.</span></a>
  <a class="umbfy-doc-card" href="insights/"><strong>Insights</strong><span>Index health, metrics, largest files, CSV export.</span></a>
  <a class="umbfy-doc-card" href="permissions/"><strong>Permissions</strong><span>Start nodes, scoped totals and what exports contain.</span></a>
</div>

## Support

Use the [UMBFY Packages issue forms](https://github.com/UMBFY/UMBFY-Packages/issues). Include the package version,
your Umbraco version and your database provider — SQL Server or SQLite matters for import questions. Never include
credentials, connection strings or licence keys in a public issue.
