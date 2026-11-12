# Bootstrap

**What it does.** Brings a near-empty destination environment up from a source snapshot in one controlled
operation, instead of promoting difference by difference.

**When to use it.** Setting up a brand-new environment — a fresh Development, Staging or disaster-recovery site —
that should start from an existing environment's schema.

**Where to find it.** **Environment Manager → Bootstrap**.

**Edition.** Professional and above.

## Why not just promote everything

On an empty destination, a normal comparison produces a very large difference set in which nearly everything is
"missing on destination". Selecting and ordering that by hand is tedious and easy to get wrong, because schema items
depend on each other and must arrive in a workable order.

Bootstrap exists for exactly that case: take a source snapshot and establish it on a near-empty destination as one
operation, with dependencies handled.

## Step-by-step

1. Confirm both environments are registered and connectivity is proven — see [Environments](environments.md).
2. Confirm the destination really is near-empty. Bootstrap is not the tool for a destination that already carries
   schema you care about.
3. Open **Environment Manager → Bootstrap**.
4. Choose the source environment and the destination.
5. Review what will be established.
6. Execute.
7. Run [verification](verification.md) against the destination.

## Understanding the result

After a successful bootstrap the destination holds the source's managed schema, and the operation is recorded in
[Deployments](deployments.md) like any other.

From that point on, keep the two environments aligned with ordinary
[compare and promotion](promotion.md) rather than repeated bootstraps.

## When not to use bootstrap

- **Not** on an established environment. For one that already has schema, compare and promote the differences —
  that way you see and approve exactly what changes.
- **Not** as a content migration. Content and media are out of scope; a bootstrapped site has schema and no
  content.
- **Not** as a backup mechanism. It is a one-directional establish from a snapshot, not a restore point.

## Limitations

- The destination must have the package installed, configured with its own identity, and be reachable.
- Schema only. See [What it moves](README.md#what-it-moves).

## Related

- [Environments](environments.md)
- [Promotion](promotion.md)
- [Verification](verification.md)
