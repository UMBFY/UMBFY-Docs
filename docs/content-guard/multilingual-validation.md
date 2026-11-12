# Multilingual Validation

**What it does.** Validates references across cultures, taking Umbraco's language fallback behaviour into account.

**Why and when to use it.** On any multilingual site. A reference that is perfectly healthy in one culture can be
broken in another, and nothing in the default editorial flow tells you.

**Where to find it.** It participates in [Publish Guard](publish-guard.md) and
[Content Health](content-health.md) rather than having a screen of its own.

**Required permissions.** Standard Umbraco permissions.

**Edition.** **Agency.**

## What it validates

| Problem | Example |
| --- | --- |
| **Missing culture** | The dependency exists, but not in the culture being published |
| **Unpublished culture** | The dependency's culture variant exists but is not published |
| **Unavailable fallback target** | Fallback is configured, but the culture it falls back to is itself missing or unpublished |

That third case is the subtle one. Language fallback makes a site look healthy by substituting another culture — and
it fails quietly when the fallback target is not there either.

## Configuration

```json
{
  "UMBFY": {
    "ContentGuard": {
      "MultilingualValidation": {
        "Enabled": true,
        "RespectLanguageFallback": true
      }
    }
  }
}
```

| Setting | Default | Effect |
| --- | --- | --- |
| `Enabled` | `true` | Whether culture-aware validation runs |
| `RespectLanguageFallback` | `true` | Whether a configured fallback counts as satisfying a reference |

Set `RespectLanguageFallback` to `false` for a stricter reading: a reference must exist **in the culture itself**,
and a fallback does not satisfy it. Useful when you want every culture genuinely translated rather than silently
falling back.

See [Configuration](configuration.md#multilingual-validation).

## Step-by-step

1. Enable multilingual validation (it is on by default).
2. Decide whether fallback should satisfy a reference — see the setting above.
3. Publish a culture variant. Culture-specific dependency problems are reported with the culture named.
4. Review site-wide culture problems in [Content Health](content-health.md).

## Understanding the result

Problems name the **culture**, not just the item. "This reference is broken" is not actionable on a six-language
site; "this reference is missing for `de-DE`" is.

Culture-specific reference *values* are handled as first-class data: a property that holds a different reference per
culture is validated per culture, not collapsed into one answer.

## Examples

**Missing translation.** A German page references a product page that exists only in English. With
`RespectLanguageFallback: true` this may be acceptable — the English content shows. With `false` it is reported, so
the team can translate it.

**Fallback chain broken.** `de-AT` falls back to `de-DE`, which has not been published. Both look fine individually;
the chain does not resolve. This is reported.

**Culture-specific picker.** A hero image differs per culture. Only the Dutch variant points at a trashed item. The
report names Dutch rather than condemning the whole page.

## Limitations

- Supported reference types only — see [Where Used](where-used.md#limitations).
- It validates references, not translation quality or completeness of body text.
- **Agency** edition. On lower editions, culture-aware validation does not run; ordinary dependency checks still do.

## Troubleshooting

| Symptom | Cause |
| --- | --- |
| No culture problems ever reported | Not on the Agency edition, or `MultilingualValidation.Enabled` is `false` |
| Fallback-satisfied references reported as problems | `RespectLanguageFallback` is `false` — that is the stricter mode working |
| A culture problem the editor cannot verify | The dependency is restricted; it is counted without revealing details |

See [Troubleshooting](troubleshooting.md).

## Related features

- [Publish Guard](publish-guard.md)
- [Content Health](content-health.md)
- [Where Used](where-used.md)
