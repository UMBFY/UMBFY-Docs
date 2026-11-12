# Safe Delete

**What it does.** Protects referenced content and media from being deleted by accident, according to a policy you
choose.

**Why and when to use it.** Because "I didn't know anything used it" is the most common cause of a broken page, and
the person deleting is rarely the person who built the page that breaks.

**Where to find it.** It acts when somebody sends a content or media item to the trash. There is no separate screen.

**Required permissions.** Whatever Umbraco already requires to delete. Safe Delete adds a check; it does not grant
anything.

**Edition.** **Free** in `Warn` mode. `RequireConfirmation` and `Block` are **Professional**.

## The three policies

| Policy | Behaviour |
| --- | --- |
| `Warn` | Allow the delete, but show what will break first |
| `RequireConfirmation` | Require an explicit, single-use confirmation. **Default** |
| `Block` | Refuse while the item is still referenced |

Configure it under `UMBFY:ContentGuard:SafeDelete` — see [Configuration](configuration.md#safe-delete).

## Step-by-step

1. An editor sends a referenced item to the trash.
2. Content Guard resolves what references it.
3. Depending on the policy, the editor is warned, asked to confirm, or refused.
4. The editor can open [Where Used](where-used.md) to see the references in full before deciding.

## Understanding the result

The dialog lists the referencing items so the decision is informed rather than a yes/no gamble. Long lists are
capped at `VisibleTake` (default 25) for readability; the total count is still reported, so an editor is never told
"3 references" when there are 300.

### Fail closed

Safety decisions **fail closed** when the dependency index is incomplete or unhealthy.

If the index is **Initializing**, **Rebuilding**, **Unhealthy** or **Failed**, Content Guard will not claim an item
is safe to delete. It would rather be cautious and occasionally inconvenient than confidently wrong — the entire
value of the feature rests on its "nothing references this" being trustworthy.

Check the state in [Content Health](content-health.md).

### Single-use confirmations

Under `RequireConfirmation`, the confirmation is explicit and single-use, and expires after
`ConfirmationTtlSeconds` (default 300). A confirmation cannot be reused for a later delete, and a stale one cannot
be replayed.

## Before you choose `Block`

`Block` is the strictest policy and it is tempting. Before you set it, understand what Content Guard can and cannot
see:

**A custom or third-party property editor is not scanned until somebody registers support for it.** Items referenced
only by such an editor look unreferenced. Under `Block` that is harmless — they simply delete. But the inverse also
matters: `Block` makes your editorial workflow depend on the completeness of the index, so register scanners for
your custom editors first.

```csharp
builder.AddContentGuardReferenceProvider<MyEditorReferenceProvider>();
```

A pragmatic path: run `Warn` for a fortnight, see what it reports, then tighten.

## Examples

**Warn.** An editor trashes an image used by two pages. They see both, delete anyway because the pages are being
retired tomorrow. Nothing blocked, nothing surprising.

**RequireConfirmation.** The same delete requires a deliberate confirmation. Enough friction to stop an accident,
not enough to stop intent.

**Block.** The delete is refused. The editor removes the two references first, then the delete succeeds.

## Limitations

- Supported reference types only — see [Where Used](where-used.md#limitations).
- Safe Delete covers deletion. Publishing is [Publish Guard](publish-guard.md); they are independent switches.
- It does not version or back up content. Umbraco's own recycle bin and versioning still apply.

## Troubleshooting

| Symptom | Cause |
| --- | --- |
| A configured `Block` behaves as `Warn` | Free edition. Licensing downgrades rather than blocks — see [Editions](editions.md) |
| Deletes are refused on an apparently unreferenced item | The index is not **Ready**, so Safe Delete failed closed |
| A delete went through that should have been caught | The reference came from an unscanned property editor |
| The site refuses to start after editing settings | A TTL outside 30–3600, a `VisibleTake` outside 1–100 or an unknown policy name is a startup error, by design |

See [Troubleshooting](troubleshooting.md).

## Related features

- [Where Used](where-used.md)
- [Publish Guard](publish-guard.md)
- [Impact](impact.md)
