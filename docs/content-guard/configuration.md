# Content Guard Configuration

All options live under `UMBFY:ContentGuard`. Every setting is optional and the defaults are production-safe; change
them only when you want a different editorial policy.

## Full example

```json
{
  "UMBFY": {
    "ContentGuard": {
      "Enabled": true,
      "SafeDelete": {
        "Enabled": true,
        "Policy": "RequireConfirmation",
        "ConfirmationTtlSeconds": 300,
        "VisibleTake": 25
      },
      "PublishGuard": {
        "Enabled": true,
        "Policy": "RequireConfirmation",
        "ConfirmationTtlSeconds": 300,
        "VisibleTake": 25
      },
      "MultilingualValidation": {
        "Enabled": true,
        "RespectLanguageFallback": true
      }
    }
  }
}
```

Environment-variable form uses the standard .NET double-underscore separator:

```bash
UMBFY__ContentGuard__SafeDelete__Policy=Block
```

## `Enabled`

Default `true`. The master switch for Content Guard.

## Policies

Both guards share one policy model:

| Policy | Behaviour |
| --- | --- |
| `Warn` | Allow the action, but show what will break |
| `RequireConfirmation` | Require an explicit, single-use confirmation. **Default** |
| `Block` | Refuse while the item is still referenced or unhealthy |

## Safe Delete

`UMBFY:ContentGuard:SafeDelete`

| Setting | Default | Purpose |
| --- | --- | --- |
| `Enabled` | `true` | Whether Safe Delete runs |
| `Policy` | `RequireConfirmation` | `Warn`, `RequireConfirmation` or `Block` |
| `ConfirmationTtlSeconds` | `300` | How long a single-use confirmation stays valid |
| `VisibleTake` | `25` | How many referencing items are listed in the dialog |

See [Safe Delete](safe-delete.md).

## Publish Guard

`UMBFY:ContentGuard:PublishGuard`

| Setting | Default | Purpose |
| --- | --- | --- |
| `Enabled` | `true` | Whether Publish Guard runs |
| `Policy` | `RequireConfirmation` | `Warn`, `RequireConfirmation` or `Block` |
| `ConfirmationTtlSeconds` | `300` | How long a single-use confirmation stays valid |
| `VisibleTake` | `25` | How many problems are listed in the dialog |

See [Publish Guard](publish-guard.md).

## Multilingual Validation

`UMBFY:ContentGuard:MultilingualValidation`

| Setting | Default | Purpose |
| --- | --- | --- |
| `Enabled` | `true` | Whether culture-aware validation runs |
| `RespectLanguageFallback` | `true` | Whether a configured fallback satisfies a reference |

See [Multilingual Validation](multilingual-validation.md).

## The three feature switches are independent

Safe Delete, Publish Guard and Multilingual Validation are configured separately and do not imply one another. A
common arrangement is a strict delete policy with a permissive publish policy, because a bad publish is reversible
and a bad delete is less so.

## Invalid configuration fails at startup

Content Guard validates its options when the site starts, and **stops the site with a configuration error** rather
than quietly substituting a default:

- a `ConfirmationTtlSeconds` outside **30–3600**
- a `VisibleTake` outside **1–100**
- an unknown policy name

This is deliberate. A typo in a policy name that silently fell back to `Warn` would leave a site less protected than
its operator believed.

## `VisibleTake` and totals

`VisibleTake` caps how many items are *listed* in a dialog, for readability. The **total count is still reported**,
so an editor is never shown "3 references" when there are 300.

## Licensing interacts with policy

Licensing **downgrades, it never blocks**:

- On a Free installation, a configured `Block` behaves as `Warn`.
- Publish Guard stands down entirely rather than refusing to publish.

So a configured policy is a ceiling, not a guarantee — check the edition if a policy seems not to apply. See
[Editions](editions.md).

## Custom property editors

A custom or third-party property editor is not scanned until support is registered:

```csharp
builder.AddContentGuardReferenceProvider<MyEditorReferenceProvider>();
```

Until then, items referenced only by that editor look unreferenced. Register your providers before tightening a
policy to `Block`. Custom reference providers are an **Agency** capability.

## Next

- [Editions](editions.md)
- [Rebuild Index](rebuild-index.md)
- [Troubleshooting](troubleshooting.md)
