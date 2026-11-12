# Replace File

**What it does.** Swaps the file behind an existing media item while keeping the item itself — so everything that
references it keeps working.

**Why and when to use it.** A corrected PDF, a re-exported logo, a photo with the right crop. The alternative —
upload a new item and repoint every reference — is slower and easy to get half-done.

**Where to find it.** Right-click a media item → **Replace file…**.

**Required permissions.** Media section access and permission on that item. Your site's own upload rules are
enforced.

## What is kept and what can change

| Kept | May change |
| --- | --- |
| The media item and its key | The file URL |
| Every reference to the item | Crops and focal points |
| The item's name and properties | Dimensions, size, fingerprint |

!!! warning "URLs and crops can change"
    Keeping the item is not the same as keeping the URL. A replacement file can produce a different URL, and crops
    or focal points set against the old dimensions may no longer be right. **The dialog warns you before you
    commit** — read it rather than clicking through.

If a page hard-codes a media URL rather than referencing the item, that link can break. Referencing the item is the
supported pattern.

## Step-by-step

1. Right-click the media item and choose **Replace file…**.
2. Choose the replacement file.
3. Read the warning about URLs and crops.
4. Confirm.
5. Check the places that use the item — especially any crop that was tuned to the old dimensions.

With [Content Guard](../content-guard/README.md) installed,
[Where Used](../content-guard/where-used.md) tells you exactly which pages to check in step 5.

## Site upload rules are enforced

A replacement goes through the same validation as any upload. Your allowed file types and size limits apply — you
cannot use Replace file to get a disallowed file into the library.

## Understanding the result

**A page now shows the new file.** The normal outcome; the reference was to the item, and the item stayed.

**A crop looks wrong.** The replacement has different dimensions. Re-set the crop or focal point. This is the case
the dialog warns about.

**A hard-coded URL broke.** The link referenced a URL rather than the item. Change it to reference the item.

## Consolidating duplicates

Replace file is a good way to resolve a duplicate group without deleting anything risky: pick the item whose
references you want to keep, replace its file with the version you want to standardise on, and the surplus items can
be retired on your own schedule. See [Duplicates](duplicates.md).

## Limitations

- URLs, crops and focal points can change. There is no way around that; it is a different file.
- Hard-coded media URLs are not updated for you.
- It replaces the file, not the item's properties. Name, alt text and other fields stay as they were.

## Related features

- [Duplicates](duplicates.md)
- [Bulk Operations](bulk-operations.md)
- [Where Used](../content-guard/where-used.md) — with Content Guard installed
