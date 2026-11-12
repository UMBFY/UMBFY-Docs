# Smart Media Picker

**What it does.** A property editor that lets editors pick existing media, upload files, upload a folder, or drag
and drop — without leaving the page they are editing.

**Why and when to use it.** The default flow is: leave the page, go to Media, upload, come back, find the item,
select it. On a content-heavy build that friction is the reason editors batch up uploads and lose track of them.

**Where to find it.** **Settings → Data Types** → the **UMBFY Smart Media Picker** data type. Add it to a property
like any other.

**Required permissions.** Media section access to upload. Your site's upload rules are enforced.

## It stores native Media Picker values

This is the part that matters architecturally, and it is the reason adopting it is low-risk:

- values are **native Media Picker values**
- **Razor** keeps working unchanged
- the **Delivery API** keeps working unchanged
- **crops and focal points** keep working unchanged
- you can **swap back to the stock picker at any time without migrating data**

There is no proprietary value format to be stuck with. If the package is removed, switch the property back to the
stock Media Picker and carry on.

## Step-by-step: add it to a document type

1. **Settings → Data Types** and locate **UMBFY Smart Media Picker**.
2. Configure it as you would a Media Picker.
3. Add it to the document type property where editors need upload-in-place.
4. Open a content item and confirm the editor can pick, upload a file, upload a folder and drag and drop.

## What editors can do from the content editor

| Action | Result |
| --- | --- |
| Pick existing media | The same as the stock picker |
| Upload one or more files | Created in Media, then selected |
| Upload a folder | Hierarchy preserved, as [folder import](upload-folders.md) |
| Drag and drop | Uploaded and selected |

Everything created this way is **ordinary Umbraco media** in the Media library — not a parallel store.

## The caveat worth knowing

The Smart Media Picker uses a **package modal override on the same alias** as the stock picker.

Two consequences for an architect:

1. **Preserve selection values.** They are native, so this is normally automatic, but do not transform them.
2. **Re-validate after an Umbraco upgrade.** A modal override against a core alias is the kind of integration that
   an upgrade can move underneath you. Include it in your post-upgrade smoke test.

## Understanding the result

**An upload appears in Media in an unexpected folder.** Check the data type's configured start node and the
destination behaviour — the picker creates media where it is configured to, not where the content item lives.

**A file is rejected.** Site upload rules are enforced. The picker is not a way around allowed file types or size
limits.

## Limitations

- Modal override on the same alias — re-validate after Umbraco upgrades.
- It does not replace Umbraco's permissions model. An editor without Media access cannot upload through it.
- Folder upload from here is subject to the same import limits and the same SQLite caveat as
  [folder import](upload-folders.md).

## Related features

- [Folder Import](upload-folders.md)
- [Collections](collections.md)
- [Permissions](permissions.md)
