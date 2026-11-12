# Duplicates

**What it does.** Groups byte-identical media using a streaming SHA-256 fingerprint.

**Why and when to use it.** Libraries accumulate the same file uploaded four times under four names. Finding them
is the first half of cleaning up; the second half is yours.

**Where to find it.** The **duplicates** smart collection in [Collections](collections.md), and the duplicate
groups report in [Insights](insights.md).

**Required permissions.** Media section access.

## Nothing is deleted for you

Media Order reports duplicate groups. It does not delete, merge or repoint anything.

That is deliberate. Deleting media is close to irreversible and the "right" copy to keep is a judgement — the one
with the better name, or the one actually referenced by a page. A tool that guessed would eventually guess wrong on
something that mattered.

Before deleting a copy, check what references it. With [Content Guard](../content-guard/README.md) installed,
[Where Used](../content-guard/where-used.md) answers that directly.

## How the fingerprint works

Files are hashed with **streaming SHA-256** after save and move, **off the request path**, so browsing is never
blocked by hashing. Concurrency is `HashingConcurrency` (2 by default) and work is batched by `IndexBatchSize`.

Files larger than `MaxIndexedFileSizeBytes` (100&nbsp;MB by default) are **not hashed**. They remain ordinary media
but have no fingerprint, so they never appear in a duplicate group. If duplicate detection on very large video
matters to you, raise the limit deliberately and expect the I/O cost.

## Binary, not perceptual

Duplicate detection is **exact and binary**. Two files are duplicates when their bytes are identical.

It will **not** find:

- the same photograph re-exported at a different quality
- a resized or cropped version
- the same image converted between formats

Perceptual similarity is an extension point only, not a feature. Do not plan a cleanup around it.

## Step-by-step

1. Open **Media → Collections** and the **duplicates** collection — or **Insights** for the groups report.
2. Review each group. Decide which copy is the keeper, usually the best-named one or the one in the right folder.
3. For each copy you plan to remove, check what references it first.
4. Repoint references to the keeper.
5. Delete the surplus copies yourself.

Alternatively, keep both and use [Replace file](replace-file.md) on the keeper so every existing reference survives
pointing at the right bytes.

## Understanding the result

**No duplicates reported on a library you know has them.** Three possibilities, in order: the index is still warming
up (check [Insights](insights.md)); the files are above `MaxIndexedFileSizeBytes`; or they are not actually
byte-identical — see "binary, not perceptual" above.

**A group containing files you expected to differ.** They are byte-identical. Different names and folders do not
make different files.

## Limitations

- Binary matching only.
- Files above `MaxIndexedFileSizeBytes` have no fingerprint.
- Requires `DuplicateDetectionEnabled` and `MetadataIndexingEnabled`.
- On a multi-server installation, hashing coordination needs a **shared database**.

## Related features

- [Insights](insights.md) — the duplicate groups report and CSV export
- [Replace File](replace-file.md) — consolidate onto one item instead of deleting
- [Collections](collections.md)
