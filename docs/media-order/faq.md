# Media Order FAQ

**Does it replace Umbraco's Media section?**
No. It adds to it. The native tree, upload pipeline and permissions model are untouched, and anything Media Order
creates is ordinary Umbraco media.

**Why do my filters do nothing in Browse?**
Because the advanced filters run in **Collections**. Browse is Umbraco's list with the Media Order toolbar on top.
Use **Apply in Collections** to carry a filter over. This is the single most common question about the package.

**Do I need Content Guard?**
No. It is an optional soft integration. With it, Media Order can answer "which media is potentially unused?";
without it, that one query returns empty rather than inventing usage. Everything else works the same.

**Why does Insights show fewer items than I have?**
The metadata index is built in the background after install. Hashing runs off the request path, so you can browse
while totals climb. Rebuild only if it has genuinely stalled.

**Do Insights totals tell me my disk usage?**
No. They are **logical indexed sizes**, not guaranteed physical disk usage. Use your storage provider's reporting
for disk.

**Will it delete my duplicates for me?**
No, deliberately. It reports byte-identical groups and leaves the decision to you — deleting media is close to
irreversible and which copy to keep is a judgement call.

**Why didn't it find two obviously-similar images?**
Detection is **binary** SHA-256: identical bytes. A re-export, a resize or a format conversion is a different file.
Perceptual similarity is an extension point only, not a feature.

**Why are some large files never fingerprinted?**
Files above `MaxIndexedFileSizeBytes` (100&nbsp;MB by default) are not hashed, so a handful of huge videos cannot
dominate the index. They stay ordinary media but do not participate in duplicate detection.

**Can a folder import overwrite my existing media?**
No. Name clashes are resolved when the import is **planned**, before anything is written. Nothing is ever
overwritten.

**Why did my folder import stall on SQLite?**
A known SQLite limitation — Umbraco's own cache sync can stall under sustained media creation. Use SQL Server for
large imports, or import in smaller batches.

**Does replacing a file break my references?**
References to the **item** survive, because the item is kept. URLs, crops and focal points can still change, and
the dialog warns you first. A page that hard-codes a media URL rather than referencing the item can break.

**Is the Smart Media Picker a proprietary value format?**
No, and this is the point of it. It stores **native Media Picker values**, so Razor, the Delivery API, crops and
focal points keep working and you can swap back to the stock picker at any time without migrating data.

**What should I watch after an Umbraco upgrade?**
The Smart Media Picker, which uses a package modal override on the same alias as the stock picker. Put it in your
post-upgrade smoke test.

**Can an editor see media outside their start node?**
No. Restricted editors see their own folders, and their totals are labelled as scoped. Rebuild index additionally
requires unrestricted media access.

**Is a bulk operation a way around permissions?**
No. Each item is authorized individually, so a bulk action can never do what the user could not do one at a time.

**Do CSV exports leak anything?**
They contain only media the current user can access and never include storage paths. They are built to be safe to
hand over.

**Does it need Node.js?**
No. Compiled Backoffice assets ship in the package.

**Does it work on a load-balanced site?**
Yes. Hashing coordination uses the package's own status rows, so all nodes need a **shared database**. No other
configuration is required.

**Which Umbraco versions are supported?**
17.x and 18.x (`[17.0.0,19.0.0)`). See
[Supported Umbraco versions](../getting-started/supported-umbraco-versions.md).

**Where do I report a bug?**
The [UMBFY Packages issue tracker](https://github.com/UMBFY/UMBFY-Packages/issues). Include your database provider
for anything import-related, and never include secrets.
