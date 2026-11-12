# Folder Import

**What it does.** Uploads a whole folder into the Media library with its hierarchy intact, with conflict handling,
a preview, live progress and a report.

**Why and when to use it.** Migrating a client's asset folder, or any upload where "drag 400 files in and sort them
out later" is not a plan.

**Where to find it.** Right-click the **Media root** or any folder → **Import folder…**.

**Required permissions.** Media section access and permission on the destination.

**Requires** `FolderImportEnabled` (on by default).

## Nothing is ever overwritten

Name clashes are resolved **when the import is planned**, before anything is written. There is no code path in which
an existing media item is silently replaced.

## What you choose

| Choice | Options |
| --- | --- |
| Destination | Media root or any folder |
| Include the top folder? | Yes — create it; no — import its contents directly |
| Folder name clashes | **merge** into the existing folder, create a **unique name**, or **skip** |
| File name clashes | **rename**, **keep both**, or **skip** |

## What you get

- a **preview tree** of exactly what will be created, before it is
- **live progress** as it runs
- **cancel** mid-import
- **retry failed** for the items that did not make it
- a **CSV report** of the outcome

## Step-by-step

1. Right-click the Media root or the destination folder and choose **Import folder…**.
2. Select the folder.
3. Choose whether to include the top folder.
4. Choose the clash behaviour for folders and for files.
5. **Read the preview tree.** This is where you catch a wrong destination, before writing anything.
6. Start the import and watch progress.
7. If anything failed, use **retry failed**.
8. Download the CSV report.

## Large imports want SQL Server

!!! warning "SQLite limitation"
    On SQLite, Umbraco's own cache sync can stall under sustained media creation. This is an Umbraco/SQLite
    characteristic rather than a Media Order defect, but it is your import that stalls.

    Use **SQL Server** for large imports. On SQLite, import in smaller batches and verify as you go.

## Limits

| Setting | Default |
| --- | --- |
| `MaxImportFiles` | 1000 |
| `MaxImportFolders` | 250 |
| `MaxImportDepth` | 10 |
| `ImportUploadConcurrency` | 3 |

These are guard rails, not aspirations. Raise them deliberately and read the SQLite note first. See
[Configuration](configuration.md#folder-import-limits).

## Understanding the result

**Items skipped.** Your clash setting said skip, or they were outside your permissions.

**Some items failed.** Use **retry failed**, then read the CSV report for the ones that still did not land — usually
a disallowed file type or a size limit.

**A clash appeared that the preview did not show.** Conflicts are resolved at plan time. If somebody else created a
media item during your import, that new item is not re-checked. Nothing is overwritten, so the result is safe — just
not what the preview predicted. Re-run for the remainder.

## After the import

Imported media is **ordinary Umbraco media**. It is indexed in the background like anything else, so give
[Insights](insights.md) a moment before judging the totals, and expect [duplicates](duplicates.md) to surface if the
source folder had any.

## Limitations

- Conflicts are resolved at plan time; concurrent creations are not re-checked.
- Large imports need SQL Server in practice.
- It creates media; it does not update any content that might want to reference it.

## Related features

- [Smart Media Picker](smart-media-picker.md) — folder upload from inside the content editor
- [Insights](insights.md)
- [Duplicates](duplicates.md)
