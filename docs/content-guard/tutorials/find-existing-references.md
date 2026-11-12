# Tutorial: Find existing references

**Goal.** Answer "what uses this?" for a specific content or media item, with enough detail to act on.

**Scenario.** Marketing wants to retire an old campaign image. Before you remove it you need to know which pages
show it, and where in those pages.

**Time.** A few minutes. **Edition.** Free.

## Before you start

Check the dependency-index state on [Content Health](../content-health.md). If it is **Initializing**,
**Rebuilding**, **Unhealthy** or **Failed**, results are incomplete and Content Guard says so — wait for **Ready**
before drawing conclusions. Do not rebuild unless diagnostics indicate it is necessary; rebuilding is not a routine
step.

## Steps

1. Open the target item — the campaign image, in **Media**.
2. Switch to the **Where Used** view.
3. Read each row. A row is one *reference*, not one item, and tells you:
     - the **source** item that references it
     - the **property** the reference came from
     - its **path** in the tree
     - its **culture / segment** where relevant
     - its **state** — published, unpublished, trashed
4. Page through long lists with the pager at the bottom, and raise **Per page** if you want fewer clicks.
5. Follow a row to open an authorized source item and see the reference in context.
6. If you need more than direct inbound references, open [Impact](../impact.md) for outbound relationships, bounded
   depth and a risk rating.

## Reading the result

**Three rows, one of which is a footer.** Now you know the image is not only on campaign pages — the property column
told you something the content tree would not have.

**A count higher than the rows shown.** Some references are from content you are not permitted to see. They are
counted without being revealed, which is the information you need in order not to break them.

**An empty list on a Ready index.** Nothing in the supported reference types points at this item. That is a real
signal — with one caveat below.

## If Where Used looks incomplete

Two causes, in order of likelihood:

1. **The index is not Ready.** Check [Content Health](../content-health.md).
2. **An unscanned property editor holds the reference.** Content Guard detects Content Picker, media references,
   Multi URL Picker internal links, Rich Text internal links, and those same editors nested in Block Grid /
   Block List. A custom or third-party editor is not scanned until support is registered — see
   [Where Used limitations](../where-used.md#limitations).

## Next

- [Protect content before deletion](protect-content-before-delete.md) — act on what you just found
- [Where Used](../where-used.md)
- [Impact](../impact.md)
