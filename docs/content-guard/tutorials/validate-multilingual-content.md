# Tutorial: Validate multilingual content

**Goal.** Publish a culture variant without leaving gaps that only show in that language.

**Scenario.** The German site is going live. English publishes cleanly, which is exactly why nobody has noticed that
two referenced items have no German variant.

**Time.** 10–20 minutes on a typical site. **Edition.** Agency, for culture-aware validation.

## Before you start

- Confirm the dependency index is **Ready** on [Content Health](../content-health.md).
- Know your `RespectLanguageFallback` setting — it changes what counts as a problem. See
  [Multilingual Validation](../multilingual-validation.md).

## Steps

1. Open [Content Health](../content-health.md) and filter the findings by culture where that helps.
2. Review **missing** and **unpublished** target-language findings. These are the two that produce visible gaps.
3. For each finding, check the dependency itself:
     - does the target culture **exist** on it?
     - is that culture **published**?
4. Review your configured **language fallback** behaviour for the culture you are publishing. A site can look
   healthy because fallback is substituting another culture — and fail quietly when the fallback target is itself
   missing or unpublished.
5. Correct the affected content or the dependency: translate it, publish the culture variant, or repoint the
   reference.
6. Re-check Content Health, or publish and let [Publish Guard](../publish-guard.md) confirm. Problems are reported
   with the **culture named**, which is what makes them actionable on a multi-language site.

## Reading the result

**Missing culture.** The dependency exists but not in the culture being published. Acceptable with
`RespectLanguageFallback: true` if fallback content is genuinely good enough; otherwise translate it.

**Unpublished culture.** The variant exists but is not live. Publish the dependency first.

**Unavailable fallback target.** The subtle one. `de-AT` falls back to `de-DE`, and `de-DE` is not published. Each
looks fine on its own; the chain does not resolve. Publish the fallback target.

**Nothing reported at all.** Either the installation is not on the Agency edition, or
`MultilingualValidation.Enabled` is `false`. Culture-aware validation does not run in either case, while ordinary
dependency checks still do.

## Choosing your strictness

| `RespectLanguageFallback` | Meaning |
| --- | --- |
| `true` (default) | A configured fallback satisfies a reference |
| `false` | A reference must exist **in the culture itself** |

Set it to `false` when you want every culture genuinely translated rather than silently falling back. Expect more
findings — that is the point.

## A note on permissions

Restricted culture details are not exposed to users who may not see them. A culture problem can therefore be
reported to an editor who cannot verify it directly; the count is the signal, and an administrator can see the rest.

## Next

- [Multilingual Validation](../multilingual-validation.md)
- [Publish Guard](../publish-guard.md)
- [Content Health](../content-health.md)
