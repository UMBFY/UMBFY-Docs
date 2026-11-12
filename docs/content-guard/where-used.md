# Where Used

**What it does.** Lists every authorized content or media item that references the item you are looking at.

**Why and when to use it.** Before changing, moving, unpublishing or deleting anything shared. "Is this logo used
anywhere?" is a question editors otherwise answer by guessing.

**Where to find it.** The **Where Used** view on any content or media item's workspace.

**Required permissions.** Standard Umbraco permissions. Where Used never reveals items the current user is not
allowed to see.

**Edition.** **Free.** Where Used is available on every installation, licensed or not.

## Step-by-step

1. Open any content or media item.
2. Switch to the **Where Used** view.
3. Read the list of inbound references.
4. Use the pager at the bottom for long lists — it has page numbers and a **Per page** choice.
5. Follow a row to open the referencing item.

## Understanding the result

Each row describes one reference, not just one item:

| Column | What it tells you |
| --- | --- |
| Source | The item that references this one |
| Property | Which property the reference came from, so you know where to look |
| Path | Where the source sits in the tree |
| Culture / segment | For culture-specific references, which variant holds it |
| State | Published, unpublished, trashed |

The property context matters. "Home references this image" is less useful than "Home → Hero → Background image
references this image", which tells the editor exactly what to change.

### Restricted references

If an item is referenced by content the current user may not see, that reference is **counted but not revealed**.
The editor learns that something they cannot see depends on this item — which is what they need in order not to
break it — without the names leaking.

This is why a count can legitimately exceed the number of visible rows.

### The index must be ready

Where Used reads the durable dependency index. While the index is **Initializing** or **Rebuilding**, results are
incomplete and Content Guard says so rather than presenting a short list as the whole truth.

Check the state in [Content Health](content-health.md); see [Rebuild Index](rebuild-index.md) if it is stuck.

## Examples

**Before deleting a shared image.** Open the image in Media, read Where Used. Three pages reference it — and the
property column shows one is a page footer, which you would not have guessed from the content tree.

**Before renaming a landing page.** Where Used shows which navigation items and rich-text links point at it, so you
can decide whether a rename is safe or needs redirects.

**Auditing an orphan.** An empty Where Used on a **Ready** index means nothing in the supported reference types
points at this item. That is a real signal — but read the limitation below first.

## Limitations

- **Only supported reference types are detected.** Content Picker, media references, Multi URL Picker internal
  links, Rich Text internal links, and those same editors nested in Block Grid / Block List. Culture-specific values
  are handled.
- **External URLs are not internal dependencies** and are not reported as such.
- **A custom or third-party property editor is not scanned** until somebody registers support for it. Until then, an
  item referenced *only* by that editor looks unreferenced. This matters a great deal before you set a delete policy
  to `Block` — see [Safe Delete](safe-delete.md#before-you-choose-block).
- Where Used reports inbound references. For outbound relationships and risk rating, use [Impact](impact.md).

## Troubleshooting

| Symptom | Cause |
| --- | --- |
| Empty for an item you know is linked | The link comes from a property editor with no scanner registered |
| Only the first few rows appear | Use the pager; it is paged, not truncated |
| Results look incomplete | The index is not **Ready** — check [Content Health](content-health.md) |

See [Troubleshooting](troubleshooting.md).

## Related features

- [Impact](impact.md) — outbound relationships and risk
- [Safe Delete](safe-delete.md) — acts on the same reference data
- [Content Health](content-health.md) — the same picture site-wide
