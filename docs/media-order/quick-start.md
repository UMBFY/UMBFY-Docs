# Media Order Quick Start

About ten minutes. It ends with a real filter, a real folder import and an understanding of the one thing that
confuses everybody.

**Before you start:** the package installed and the site restarted. See [Installation](installation.md).

## 1. Check the index

Open **Media → Insights**.

The metadata index is built in the background after install. While it warms up, advanced sorts fall back safely and
Insights totals climb as items are read. You can work during this — hashing is off the request path — but the
numbers are not final yet.

[More on Insights →](insights.md)

## 2. Learn Browse vs Collections now

This is the one piece of knowledge that saves you a confused half-hour:

| Where | What it is |
| --- | --- |
| **Media → Browse** | Umbraco's own list, with the Media Order toolbar on top |
| **Media → Collections** | Where the **advanced filters actually run**, plus smart collections, saved searches and bulk actions |

If you build a filter in Browse and nothing seems to happen, that is why. Use **Apply in Collections** to carry it
over.

## 3. Sort the library properly

In **Browse**, use the toolbar to sort by upload date, name, file size, dimensions, resolution, extension or media
type.

Changing the sort resets paging to the first page — deliberately, so you are not left on page 7 of a different
ordering.

Upload something. It appears at the **top**, because the default sort is Upload Date descending.

[More on Sorting and Filtering →](sorting.md)

## 4. Run a real filter in Collections

Open **Media → Collections** and build something you actually want to know, for example:

- images over 2&nbsp;MB
- items with missing metadata
- duplicates

Then **save the search**. Saved searches are per user, so your colleagues are not affected by your experiments.

[More on Collections →](collections.md)

## 5. Look at duplicates

Open the **duplicates** smart collection. Byte-identical files are grouped by SHA-256 fingerprint.

**Nothing is deleted for you.** You get the groups and decide — which is the right behaviour for something as
irreversible as deleting media.

[More on Duplicates →](duplicates.md)

## 6. Import a folder

Right-click the Media root or a folder and choose **Import folder…**.

You choose the destination, whether to include the top folder, and what to do about name clashes — merge, unique
name or skip for folders; rename, keep both or skip for files. You get a preview tree, live progress, cancel,
retry-failed and a CSV report.

**Nothing is ever overwritten.** Clashes are resolved when the import is planned.

!!! warning "Large imports want SQL Server"
    On SQLite, Umbraco's own cache sync can stall under sustained media creation. Try a small folder first if you
    are on SQLite.

[More on Folder Import →](upload-folders.md)

## 7. Try a bulk rename

In **Collections**, select several items and start a bulk rename. You get a **preview** before anything is applied.

Per-item authorization applies, so a bulk action can never do what the user could not do one item at a time.

[More on Bulk Operations →](bulk-operations.md)

## 8. Replace a file without breaking references

Right-click a media item and choose **Replace file…**.

The media **item** is kept, so references to it survive. URLs and crops can still change — the dialog warns you
before you commit.

[More on Replace File →](replace-file.md)

## 9. Optional: let editors upload from the content editor

Add the **UMBFY Smart Media Picker** data type (**Settings → Data Types**) to a property. Editors can then pick,
upload files, upload a folder or drag and drop without leaving the page.

It stores **native Media Picker values**, so Razor, the Delivery API, crops and focal points keep working and you
can swap back to the stock picker at any time without migrating data.

[More on the Smart Media Picker →](smart-media-picker.md)

## If "potentially unused" returns nothing

That query needs [Content Guard](../content-guard/README.md). Without it, Media Order returns empty rather than
guessing at usage it cannot see. Everything else works without it.

## Next

- [Configuration](configuration.md) — all 21 options
- [Permissions](permissions.md) — start nodes and scoped totals
- [FAQ](faq.md)
