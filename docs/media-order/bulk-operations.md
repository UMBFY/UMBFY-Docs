# Bulk Operations

**What it does.** Rename, move, and add or remove favourites across many media items at once — with a preview
before a rename is applied.

**Where to find it.** Select items in [Collections](collections.md).

**Required permissions.** Media section access, **and the permission to do the same thing to each individual item**.

## Per-item authorization

A bulk operation is not a privilege escalation. Each item is authorized individually, so a bulk action can never do
something the user could not have done one item at a time.

The practical effect for an editor with a restricted media start node: selecting broadly and acting is safe, because
items outside their scope are not acted on.

## Rename with a preview

Renaming many files is the operation people get wrong, so it has a preview step: you see the proposed new names
**before** anything is applied, and can go back.

Use it. A rename across 300 items is not something to run hopefully.

## Move

Move the selection to another folder. Umbraco's own rules apply — Media Order does not bypass the Media tree or its
permissions.

## Favourites

Add or remove favourites in bulk. Favourites are per user, so this affects your own view only. Requires
`FavoritesEnabled`.

## Step-by-step

1. Open **Media → Collections**.
2. Filter to the set you want — this is why the filters matter; a precise selection is a safe bulk operation.
3. Select the items.
4. Choose the action.
5. For a rename, **read the preview**, then apply.
6. Check the result.

## Batch limits

`MaxBatchSize` bounds a single operation at **100** items by default. For a larger job, narrow the filter and run
it in passes rather than raising the limit on a production site — each pass is verifiable.

See [Configuration](configuration.md#paging-and-batching).

## Understanding the result

**Fewer items changed than selected.** Expected when some were outside your permissions — per-item authorization
at work.

**A rename preview that looks wrong.** Go back and adjust. That is the entire purpose of the step.

## Limitations

- `MaxBatchSize` caps one operation; default 100.
- Bulk delete is not a Media Order operation. Deleting media stays with Umbraco's own flow, deliberately — see
  [Duplicates](duplicates.md#nothing-is-deleted-for-you) for the reasoning.
- Moving does not update references. If a reference depends on a path, check it afterwards; with
  [Content Guard](../content-guard/README.md) installed,
  [Where Used](../content-guard/where-used.md) tells you what points at an item.

## Related features

- [Collections](collections.md)
- [Replace File](replace-file.md)
- [Permissions](permissions.md)
