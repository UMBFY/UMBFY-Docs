# Tutorial: Protect content before deletion

**Goal.** Remove an item without breaking the pages that use it.

**Scenario.** A product has been discontinued and its page should go. Three other pages link to it, one of which
nobody remembers building.

**Time.** Depends on what you find. **Edition.** Free for the review and a `Warn` delete; stricter policies are
Professional.

!!! note "This is not a governance process"
    Content Guard tells you what references an item. Whether the item *should* be removed, and who signs that off,
    remains your organisation's decision.

## Before you start

Confirm the dependency index is **Ready** on [Content Health](../content-health.md). A delete decision taken from an
incomplete index is the one case this tool is meant to prevent — and the guards will fail closed rather than let you
take it.

## Steps

1. Open the item you plan to remove.
2. Open **Where Used** and read every inbound reference, including the property each came from.
3. Open [Impact](../impact.md) if you want the broader picture — outbound relationships and a risk rating.
4. **Deal with the references first.** For each one, either:
     - repoint it at a replacement item, or
     - remove the reference from the source page, or
     - decide deliberately that the source page is being retired too.
5. Re-check **Where Used**. On a **Ready** index it should now be empty, or contain only references you have
   consciously accepted.
6. Perform the delete.
7. Read the Safe Delete result and follow your configured policy:
     - **`Warn`** — you are shown what will break and the delete proceeds
     - **`RequireConfirmation`** — confirm deliberately; the confirmation is single-use and expires
     - **`Block`** — the delete is refused while references remain

## Reading the result

**The delete was refused under `Block`.** Working as configured. Go back to step 4.

**The delete was allowed but you expected it to be blocked.** Check the edition before suspecting a bug — licensing
downgrades rather than blocks, so on a Free installation `Block` behaves as `Warn`. See
[Editions](../editions.md).

**A confirmation expired.** Confirmations are single-use and time-limited (default 300 seconds) so a stale one
cannot be replayed. Start the delete again.

## The caveat worth knowing

An item referenced **only** by a custom or third-party property editor with no scanner registered looks
unreferenced. That is the one way this workflow can tell you a delete is safe when it is not. Register scanners for
your custom editors before relying on this process — see
[Safe Delete](../safe-delete.md#before-you-choose-block).

## Next

- [Safe Delete](../safe-delete.md)
- [Find existing references](find-existing-references.md)
- [Configuration](../configuration.md#safe-delete)
