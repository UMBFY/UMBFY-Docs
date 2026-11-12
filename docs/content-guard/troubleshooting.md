# Content Guard Troubleshooting

## Check the index state first

Almost every surprising Content Guard result has one of two causes: **the index is not Ready**, or **the reference
comes from a property editor with no scanner**. Check the index state on
[Content Health](content-health.md) before investigating anything else.

| State | What it means |
| --- | --- |
| **Initializing** / **Rebuilding** | Incomplete. Guards fail closed; results are not trustworthy yet |
| **Ready** | Normal operation |
| **Unhealthy** / **Failed** | Something went wrong; the last error is recorded |

## Health says "Initializing" and never changes

**Cause.** The first build failed.

**Fix.**

1. Read the recorded last error on Content Health.
2. Check the Umbraco log for the underlying exception.
3. Confirm the package migration created its index tables — a failed migration is the usual root cause on a fresh
   install.
4. Confirm the database user can write to those tables.
5. [Rebuild the index](rebuild-index.md) (administrator required).

## Where Used is empty for an item you know is linked

**Cause.** The reference comes from a property editor with no scanner registered.

Content Guard detects Content Picker, media references, Multi URL Picker internal links, Rich Text internal links,
and those same editors nested in Block Grid / Block List. A custom or third-party editor is not scanned until
somebody registers support:

```csharp
builder.AddContentGuardReferenceProvider<MyEditorReferenceProvider>();
```

**Also check** the index is **Ready**, and that the referencing item is not simply one the current user may not see
— restricted references are counted without being revealed, so a count can exceed the visible rows.

## "Nothing references this" but deleting still broke a page

Same two causes as above: an unscanned property editor, or an index that was not **Ready** at the time.

Confirm the index state, then check whether the breaking reference came from a custom editor. This is also the
reason to read [Safe Delete](safe-delete.md#before-you-choose-block) before relying on `Block`.

## A configured `Block` policy behaves as `Warn`

**Not a bug.** Licensing downgrades rather than blocks: on a Free installation `Block` behaves as `Warn` and
[Publish Guard](publish-guard.md) stands down, so deleting and publishing keep working.

A configured policy is a ceiling, not a guarantee. Check the edition — see [Editions](editions.md).

## Publish Guard does nothing

Either the installation is on Free (where it stands down by design), or
`UMBFY:ContentGuard:PublishGuard:Enabled` is `false`. The three feature switches are independent.

## The site will not start after editing settings

**Cause.** Invalid configuration, deliberately failing at startup rather than silently falling back:

- `ConfirmationTtlSeconds` outside **30–3600**
- `VisibleTake` outside **1–100**
- an unknown policy name

**Fix.** Correct the value. The startup error names it. See [Configuration](configuration.md).

## Lists only show the first page

**Not a bug.** The lists are paged, not truncated. Use the pager at the bottom — it has page numbers and a
**Per page** choice.

## Content Health numbers look too low

**Cause.** Scope. Results are limited to what the current user may see, so an editor restricted to a subtree sees
that subtree's health.

## A culture problem is reported that looks fine

Check `RespectLanguageFallback`. With it set to `false`, a reference must exist **in the culture itself** and a
configured fallback does not satisfy it — that is the stricter mode working as asked. See
[Multilingual Validation](multilingual-validation.md).

## Guards are cautious right after an upgrade

Expected, briefly. A migration can trigger a rebuild, and the guards fail closed while the index is rebuilding.
Wait for **Ready**.

## Still stuck

Collect the Content Guard version, your Umbraco version, the index state from
[Content Health](content-health.md), and the recorded last error, then see
[Reporting Issues](../shared/reporting-issues.md) and [Diagnostics](../shared/diagnostics.md).

Never include connection strings, credentials or licence keys in a public issue — redact log excerpts first.
