# Recovery

**What it does.** Assesses what went wrong with a promotion and executes recovery for supported managed schema.

**When to use it.** After a failed execution, or after [verification](verification.md) reports a mismatch.

**Where to find it.** The deployment record for the run, under **Environment Manager → Deployments**.

**Edition.** Professional and above.

## Assess before you act

Recovery has two distinct stages, and the order matters:

1. **Assess** — read what the destination actually looks like now and what recovery would do about it.
2. **Execute** — apply the recovery.

Recovery is itself a schema mutation. It goes through the same controls as a promotion, and for the same reason:
the moment you are recovering is the moment you least want an unaudited change.

## Step-by-step

1. Open the deployment record for the affected run.
2. Run a recovery **assessment**.
3. Read the assessment, item by item.
4. If the assessment describes what you want, execute recovery.
5. Run [verification](verification.md) again afterwards.

## What recovery can and cannot reach

Recovery covers **supported managed schema** — the schema types Environment Manager promotes, as created or
modified by Environment Manager.

It is not a database restore and it is not a general undo. Specifically it does not:

- restore content or media
- undo changes made directly in the Backoffice by somebody else
- roll back application binaries or packages
- substitute for a database backup

Keep a database backup strategy. Recovery narrows the window in which a schema promotion can leave you stuck; it
does not replace your backups.

## Understanding the result

A successful recovery followed by a clean verification means the destination is back to a state you can account for.
That is the goal — not "the error message went away".

If recovery cannot reach the problem, the assessment will say so. At that point the honest options are a manual
schema correction, or restoring from backup.

## When not to use recovery

- **Do not re-execute the original plan** as a way of fixing a mismatch. Compare again, and build a new plan from
  the destination's real current state.
- Do not run recovery on a destination that somebody is actively editing. Get the environment quiet first.

## Limitations

- Supported managed schema only.
- Requires connectivity to the destination, like any other remote operation.

## Related

- [Verification](verification.md)
- [Promotion](promotion.md)
- [Troubleshooting](troubleshooting.md)
