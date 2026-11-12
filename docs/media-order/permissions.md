# Permissions

Media Order **adds to** Umbraco's Media section. It does not replace the permissions model, and it does not grant
anyone access to anything they could not already reach.

## The baseline

Everything in Media Order requires **Media section access**. No Media access, no Media Order.

## Restricted media start nodes

An editor confined to a media start node sees **only their own folders** — in Browse, in
[Collections](collections.md), in the smart collections, and in [Insights](insights.md).

Crucially, their figures are **labelled as scoped**. A total computed over a subtree says so, rather than presenting
itself as the library's total. That distinction matters the moment somebody puts a number in an e-mail.

## Rebuild index needs unrestricted access

[Rebuilding the index](insights.md#rebuilding) re-reads the **whole** library, so it requires **unrestricted** media
access.

An editor confined to a start node cannot rebuild an index spanning folders they cannot see — which is both a
permissions decision and a correctness one.

## Bulk operations are authorized per item

A [bulk operation](bulk-operations.md) authorizes **each item individually**. A bulk action can never do something
the user could not have done one item at a time.

The practical effect: selecting broadly is safe. Items outside the user's scope are not acted on, and the result
reports fewer items changed than selected.

## Folder import

Folder import requires permission on the **destination**, and the site's own upload rules — allowed file types, size
limits — are enforced exactly as for any upload. It is not a route around them.

See [Folder Import](upload-folders.md).

## Replace file

Requires permission on the item, and enforces the site's upload rules. You cannot use **Replace file…** to put a
disallowed file into the library.

See [Replace File](replace-file.md).

## Smart Media Picker

An editor needs Media access to upload through it. Media created from the content editor is ordinary Umbraco media,
subject to the same rules as anything uploaded in the Media section.

See [Smart Media Picker](smart-media-picker.md).

## CSV exports

Exports from [Insights](insights.md):

- contain only media keys the **current user** can access
- **never** include storage paths

They are built to be safe to attach to a ticket or hand to a client.

## What is deliberately not here

- **Bulk delete.** Deleting media stays in Umbraco's own flow. See
  [Duplicates](duplicates.md#nothing-is-deleted-for-you) for the reasoning.
- **Any permission of its own.** Media Order has no separate permission scheme to configure. It reads Umbraco's.

## Related

- [Insights](insights.md)
- [Bulk Operations](bulk-operations.md)
- [Configuration](configuration.md)
