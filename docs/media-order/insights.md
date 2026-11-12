# Insights

**What it does.** Reports the state of the metadata index and the shape of the library: totals, type breakdown,
largest files, missing metadata, duplicate groups, and a CSV export.

**Why and when to use it.** First stop after installing, to watch the index warm up. Afterwards, the place to answer
"what is actually in this library and what is it costing us?"

**Where to find it.** **Media → Insights**.

**Required permissions.** Media section access. **Rebuild index** requires **unrestricted** media access.

**Requires** `InsightsEnabled` (on by default).

## Index health and rebuild

The index state is the first thing to read, because the advanced sorts, filters and duplicate detection all depend
on it.

After installation the index is built in the background. While it warms up:

- advanced sorts **fall back safely** rather than showing a blank collection
- the totals here **climb as items are read**

That is the normal post-install experience, not a fault.

### Rebuilding

Rebuild re-reads the whole library, so it requires **unrestricted media access** — an editor confined to a start
node cannot rebuild an index that spans folders they cannot see.

Rebuild when the index has genuinely stalled, or after a bulk operation that bypassed normal save and move events,
such as a direct database import. It is not a routine step.

## What it reports

| Report | Use it for |
| --- | --- |
| **Totals** | Item counts and indexed size |
| **Type breakdown** | What the library is made of |
| **Largest files** | Cleanup candidates, by `LargeFileThresholdBytes` (10&nbsp;MB default) |
| **Missing metadata** | Items the index could not fully read |
| **Duplicate groups** | Byte-identical sets — see [Duplicates](duplicates.md) |
| **CSV export** | The above, for a spreadsheet or a report to a client |

## Totals are logical, not physical

!!! important "Insights totals are logical indexed sizes"
    They are **not** guaranteed physical disk usage. Treat them as a measure of what the library contains, not as a
    storage-billing figure. Your storage provider's own reporting is authoritative for disk.

This matters if you are using the number in a client conversation about hosting cost.

## Scoped totals

An editor with a restricted media start node sees figures for what they can see, and those figures are **labelled as
scoped**. A scoped total is honest about its own scope rather than presenting a subtree's numbers as the library's.

See [Permissions](permissions.md).

## CSV export

The export contains only media the current user may access, and **never includes storage paths**. It is designed to
be safe to hand to a client or attach to a ticket.

## Step-by-step: audit a library

1. Open **Media → Insights** and confirm the index is settled.
2. Read the totals and the type breakdown for the overall shape.
3. Work through **largest files** for cleanup candidates.
4. Check **duplicate groups** — nothing is deleted for you.
5. Check **missing metadata** for items that may be corrupt or unusual.
6. Export the CSV for the write-up.

## Understanding the result

**Far fewer items than you have.** The background index is still running. Check back; rebuild only if it has
genuinely stalled.

**Items permanently in "missing metadata".** They are likely above `MaxIndexedFileSizeBytes` (100&nbsp;MB default),
or are a format whose dimensions cannot be read. They remain ordinary media, and they do not participate in
duplicate detection.

**Totals lower than your storage bill.** Expected — see "logical, not physical" above.

## Limitations

- Totals are logical indexed sizes.
- Requires `MetadataIndexingEnabled`; with indexing off there is little to report.
- Rebuild requires unrestricted media access.
- On a multi-server installation, index coordination needs a **shared database**.

## Related features

- [Duplicates](duplicates.md)
- [Collections](collections.md)
- [Permissions](permissions.md)
