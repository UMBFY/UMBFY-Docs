# Rebuild Index

**What it does.** Re-reads the content and media tree and rebuilds the durable dependency index that powers every
Content Guard feature.

**Why and when to use it.** When [Content Health](content-health.md) reports the index as **Unhealthy**,
**Failed**, or stuck on **Initializing** — or after a bulk content operation that bypassed normal save events, such
as a direct database import.

**Where to find it.** The [Content Health](content-health.md) dashboard.

**Required permissions.** Backoffice **administrator**. Rebuild re-reads the whole tree.

**Edition.** Available on **every** edition, including Free. Rebuild is never licence-gated, because
[Where Used](where-used.md) is a free feature and cannot work without the index.

## You usually do not need this

Content Guard builds its index automatically on first start and maintains it as content changes. On an existing
site, **you do not need to re-save anything** after installing.

Rebuild is for the exceptions, not for routine use.

## Step-by-step

1. Open the [Content Health](content-health.md) dashboard.
2. Read the current index state and, if present, the recorded last error.
3. Start the rebuild.
4. The state moves to **Rebuilding**. On a large site this takes a few minutes.
5. Wait for **Ready**.

## While it rebuilds

The guards **fail closed**. During **Rebuilding**, Content Guard will not report an item as safe to delete or a page
as safe to publish, because the index is known to be incomplete.

Editors may therefore see more caution than usual for a few minutes. That is correct behaviour, not a fault — the
alternative is a confident wrong answer.

## Understanding the result

| After rebuild | Meaning |
| --- | --- |
| **Ready** | Normal operation; results are trustworthy |
| **Unhealthy** / **Failed** | The rebuild did not complete. The last error is recorded — read it |
| Still **Initializing** | The build is not progressing. Check the Umbraco log |

## When a rebuild keeps failing

1. Read the recorded error on Content Health first; it names the cause.
2. Check the Umbraco log for the underlying exception.
3. Confirm the package migration created its index tables — a failed migration is the usual root cause on a fresh
   install.
4. Confirm the database user can write to those tables.

## Limitations

- Rebuild re-reads supported reference types only. It cannot discover references held by an unscanned custom
  property editor — see [Where Used](where-used.md#limitations).
- It is an administrator operation and is intentionally not available to editors.

## Related

- [Content Health](content-health.md)
- [Installation](installation.md)
- [Troubleshooting](troubleshooting.md)
