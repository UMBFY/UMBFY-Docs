# Content Guard Editions

| Edition | What you get |
| --- | --- |
| **Free** | [Where Used](where-used.md), and [Safe Delete](safe-delete.md) in `Warn` mode — you always see what references an item before you change it |
| **Professional** | Free, plus Safe Delete `RequireConfirmation` / `Block`, [Publish Guard](publish-guard.md), [Content Health](content-health.md) and [Impact](impact.md) |
| **Agency** | Professional, plus [multilingual validation](multilingual-validation.md), custom reference providers and reporting |

## Licensing downgrades, it never blocks

This is the design principle worth understanding before anything else.

On a Free installation:

- a configured `Block` delete policy behaves as `Warn`
- [Publish Guard](publish-guard.md) stands down

So **deleting and publishing keep working**. Your site is never held hostage to a licence, an expired licence, or a
licensing service you cannot reach. Paid screens show what the feature needs and a link to the plans, rather than an
error.

The practical consequence for administrators: a configured policy is a **ceiling, not a guarantee**. If a `Block`
policy appears not to apply, check the edition before you go looking for a bug.

## What Free actually gives you

Free is not a teaser. [Where Used](where-used.md) is the feature editors reach for most, and it is complete on a
Free installation: full inbound references with property context, path, culture and state, permission-aware, paged.

Combined with `Warn` deletes, that is a genuinely useful safety net — you always see what references an item before
you change it.

## Index rebuild is never licence-gated

[Rebuild Index](rebuild-index.md) is available on every edition, because Where Used is free and cannot work without
the index. Gating the rebuild would gate a free feature by the back door.

It does require a Backoffice **administrator**, since it re-reads the content tree.

## Checking your edition

Licence state is reported per package in [Hub](../hub/packages.md). Hub caches and reports licence state; licences
themselves are verified offline, so an outage never grants paid access and never revokes a valid licence.

## Related

- [Configuration](configuration.md) — how policy and edition interact
- [Hub Packages](../hub/packages.md) — where licence state is shown
