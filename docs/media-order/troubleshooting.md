# Media Order Troubleshooting

## Advanced filters seem to do nothing in Browse

**Cause.** Browse is Umbraco's native list with the Media Order toolbar on top. The **advanced filters run in
Collections**.

**Fix.** Use **Apply in Collections** to carry your filter over, or build it in
[Collections](collections.md) in the first place.

This is the most common confusion with the package and it is not a fault.

## Insights shows far fewer items than you have

**Cause.** The background metadata index is still running. It is built after install, off the request path, so
browsing works while totals climb.

**Fix.** Wait and check [Insights](insights.md) again. Only [rebuild](insights.md#rebuilding) if it has genuinely
stalled — rebuild is not a routine step, and it needs unrestricted media access.

## Dimension, resolution or duplicate features are unavailable

**Cause.** They depend on the metadata index. Either it is still warming up, or `MetadataIndexingEnabled` is
`false`.

**Fix.** Check the index state in Insights; check the flag in [Configuration](configuration.md#feature-flags).

## Folder import stalls on SQLite

**Cause.** A known SQLite limitation: Umbraco's own cache sync can stall under sustained media creation. It is an
Umbraco/SQLite characteristic rather than a Media Order defect — but it is your import that stops.

**Fix.** Use **SQL Server** for large imports. On SQLite, import in smaller batches and verify as you go. See
[Folder Import](upload-folders.md#large-imports-want-sql-server).

## "Potentially unused" returns nothing

**Cause.** That query requires [Content Guard](../content-guard/README.md).

**Expected behaviour.** Without Content Guard, Media Order returns **empty rather than inventing usage** it cannot
determine. Everything else in the package works without it.

**Fix.** Install Content Guard if you want the answer, and leave
`ContentGuardIntegrationEnabled` at `true`.

## Replacing a file changed a URL

**Expected, and the dialog warns about it.** The media **item** is kept, so references to the item survive, but
URLs, crops and focal points can change — it is a different file.

**Fix.** Re-set any crop that was tuned to the old dimensions. If a page broke, it was hard-coding a media URL
rather than referencing the item; change it to reference the item. See
[Replace File](replace-file.md).

## No duplicates reported on a library that has them

Three causes, in order of likelihood:

1. The index is still warming up — check [Insights](insights.md).
2. The files are above `MaxIndexedFileSizeBytes` (100&nbsp;MB default) and therefore have no fingerprint.
3. They are **not byte-identical**. Detection is binary SHA-256, not perceptual — a re-export, a resize or a format
   conversion is a different file. See [Duplicates](duplicates.md#binary-not-perceptual).

## A bulk operation changed fewer items than I selected

**Expected.** Each item is authorized individually, so items outside your permissions are not acted on. A bulk
action never does what you could not do one item at a time.

## Totals do not match my storage bill

**Expected.** Insights totals are **logical indexed sizes**, not guaranteed physical disk usage. Your storage
provider's reporting is authoritative for disk.

## My totals look like a fraction of the library

**Cause.** A restricted media start node. You see your own folders, and the figures are **labelled as scoped**.

See [Permissions](permissions.md).

## A clash appeared that the import preview did not show

**Cause.** Folder import resolves conflicts **when it plans**. An item created by somebody else during the import is
not re-checked.

**Nothing is overwritten**, so the result is safe — just not what the preview predicted. Re-run for the remainder.

## The Smart Media Picker stopped behaving after an Umbraco upgrade

**Cause.** It uses a package modal override on the same alias as the stock picker, which an Umbraco upgrade can move
underneath.

**Fix.** Re-validate it as part of your post-upgrade smoke test, and update the package. Selection values are native
Media Picker values, so nothing needs migrating. See
[Smart Media Picker](smart-media-picker.md#the-caveat-worth-knowing).

## Multi-server: indexing looks inconsistent

**Cause.** Hashing coordination uses the package's own operation and index status rows, which requires a **shared
database**.

**Fix.** Confirm all nodes use the same database.

## Still stuck

Collect the Media Order version, your Umbraco version, **your database provider** — SQL Server or SQLite matters for
import questions — and the index state from [Insights](insights.md), then see
[Reporting Issues](../shared/reporting-issues.md) and [Diagnostics](../shared/diagnostics.md).

Never include credentials, connection strings or licence keys in a public issue.
