# Content Guard Quick Start

About ten minutes, and it ends with you having verified Content Guard against a reference you created yourself —
rather than hoping it works.

**Before you start:** the package installed and the site restarted. See [Installation](installation.md).

## 1. Wait for the index

Open the [Content Health](content-health.md) dashboard and wait for the index state to reach **Ready**.

Do not skip this. While the index is **Initializing** the guards deliberately fail closed, so anything you test
before then tells you about the index state rather than about your content.

## 2. Create a reference you control

So that step 3 proves something:

1. Pick or upload an image in **Media**.
2. Open a content page.
3. Point a media picker property at that image.
4. **Save** the page.

## 3. Verify Where Used

1. Open the image in **Media**.
2. Switch to the **Where Used** view.

You should see your content page listed, with the **property** it came from, its path, its culture where relevant,
and its state.

That property column is the point of the feature: knowing *which* property holds the reference is what makes the
fix actionable.

[More on Where Used →](where-used.md)

## 4. Review Impact before changing something shared

On the same page, open the **Impact** view (Professional and above). It shows:

- **inbound** relationships — what would break if you changed this
- **outbound** relationships — what this page depends on
- a **risk classification** for the change

Use it as a prompt to look, not as permission. [More on Impact →](impact.md)

## 5. Try a guarded delete

Send the image from step 2 to the trash.

With the default `RequireConfirmation` policy, you are shown the page that references it and asked to confirm
deliberately. Cancel.

That is Safe Delete doing its job: enough friction to stop an accident, not enough to stop intent.
[More on Safe Delete →](safe-delete.md)

## 6. Scan the site

Return to [Content Health](content-health.md) and review site-wide dependency problems — missing, trashed,
unpublished and culture-specific. Use the filters and the pager.

Remember results are scoped to what your user may see.

## 7. Decide your editorial policy

Defaults are production-safe. Change them only if you want a different policy:

| Policy | Behaviour |
| --- | --- |
| `Warn` | Allow it, but show what will break |
| `RequireConfirmation` | Require an explicit, single-use confirmation. **Default** |
| `Block` | Refuse while the item is still referenced |

Safe Delete, [Publish Guard](publish-guard.md) and
[multilingual validation](multilingual-validation.md) are independent switches — see
[Configuration](configuration.md).

!!! warning "Before you set `Block`"
    A custom or third-party property editor is not scanned until support is registered, so items referenced only by
    such an editor look unreferenced. Register your providers first — see
    [Safe Delete](safe-delete.md#before-you-choose-block).

## What you just used

| Step | Edition |
| --- | --- |
| Where Used (3) | Free |
| Guarded delete in `Warn` (5) | Free |
| Impact (4), Content Health (6), `RequireConfirmation` / `Block`, Publish Guard | Professional |
| Multilingual validation, custom reference providers | Agency |

Licensing downgrades rather than blocks, so on a Free installation the stricter policies quietly behave as `Warn`
instead of erroring. See [Editions](editions.md).

## Next

- [Tutorials](tutorials/README.md) — three focused walkthroughs
- [Configuration](configuration.md)
- [FAQ](faq.md)
