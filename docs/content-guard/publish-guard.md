# Publish Guard

**What it does.** Detects unhealthy dependencies **before** content is published, including culture-specific
problems.

**Why and when to use it.** Publishing a page whose dependencies are missing, trashed or unpublished produces a
live page with broken parts. Publish Guard reports that while it is still cheap to fix.

**Where to find it.** It acts on publish. There is no separate screen.

**Required permissions.** Whatever Umbraco already requires to publish.

**Edition.** **Professional.** On a Free installation Publish Guard stands down and publishing is unaffected.

## What it checks

| Problem | Why it matters |
| --- | --- |
| **Missing** dependency | The referenced item no longer exists |
| **Trashed** dependency | It is in the recycle bin and will not render |
| **Unpublished** dependency | It exists but is not live, so the live page gets a gap |
| **Culture-specific** problems | The dependency exists but not in the culture being published |

The culture dimension is the one teams miss. A page that publishes correctly in English can publish broken in
German because a referenced item has no German variant — see
[Multilingual Validation](multilingual-validation.md).

## The three policies

Publish Guard uses the same policy model as Safe Delete:

| Policy | Behaviour |
| --- | --- |
| `Warn` | Publish, but report the problems first |
| `RequireConfirmation` | Require an explicit, single-use confirmation. **Default** |
| `Block` | Refuse to publish while dependencies are unhealthy |

Configure it under `UMBFY:ContentGuard:PublishGuard` — see
[Configuration](configuration.md#publish-guard). It is an independent switch from Safe Delete; you can run one
strict and the other permissive.

## Step-by-step

1. An editor publishes a page.
2. Content Guard resolves its outbound dependencies and checks their state.
3. Unhealthy dependencies are reported, grouped by problem.
4. Depending on the policy, the editor is warned, asked to confirm, or refused.

## Understanding the result

Problems are listed with enough context to act on: which dependency, what is wrong with it, and in which culture.
Long lists are capped at `VisibleTake` (default 25) with the total still reported.

A clean result means no supported dependency of this item is missing, trashed, unpublished or culture-broken. It
does not mean the page is editorially correct.

### Fail closed

Like Safe Delete, Publish Guard fails closed on an incomplete or unhealthy index. It will not report a clean bill of
health from a half-built index. Check [Content Health](content-health.md).

## Examples

**Unpublished dependency.** A news article references an author page nobody published. `Warn` reports it; the editor
publishes the author first.

**Culture gap.** A German page references an item with no German variant. The English publish was fine, which is
exactly why nobody noticed. Publish Guard names the culture.

**Trashed dependency.** A page references an image someone trashed last week. Under `RequireConfirmation` the editor
confirms deliberately or fixes it — either way the breakage was not silent.

## Limitations

- Supported reference types only — see [Where Used](where-used.md#limitations).
- It checks dependency health, not rendering. A dependency that is present and published can still render wrongly.
- On a Free installation it stands down entirely, by design — licensing downgrades, it never blocks publishing.

## Troubleshooting

| Symptom | Cause |
| --- | --- |
| Publish Guard does nothing | Free edition, or `PublishGuard.Enabled` is `false` |
| It reports a problem the editor cannot see | The dependency is restricted; it is counted without revealing details |
| Publishes are refused on apparently healthy content | The index is not **Ready**, so it failed closed |

See [Troubleshooting](troubleshooting.md).

## Related features

- [Multilingual Validation](multilingual-validation.md)
- [Safe Delete](safe-delete.md)
- [Content Health](content-health.md)
