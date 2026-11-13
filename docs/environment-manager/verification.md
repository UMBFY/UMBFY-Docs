# Verification

**What it does.** Independently re-reads the destination environment after a promotion and confirms that it matches
what the plan said it would do.

**When to use it.** After **every** execution. A promotion is not complete until it has verified.

**Where to find it.** The deployment record for the run, under **Environment Manager → Activity**.

**Edition.** Professional and above.

## Why this exists as a separate step

An executor reporting its own success is weak evidence. It tells you that the execution code believed it succeeded,
which is exactly the thing that is wrong when something has gone subtly wrong.

Verification re-reads the destination from the outside and compares what is actually there against what the plan
specified. It can therefore catch:

- an item that was reported as applied but is not present
- an item that is present but does not match the planned definition
- a dependency that did not land, leaving schema that is technically present but not usable

## Step-by-step

1. Open the deployment record for the run.
2. Run **verification**.
3. Read the result per item, not just the overall status.

## Understanding the result

| Result | What it means | What to do |
| --- | --- | --- |
| Verified | The destination matches the plan | Nothing. The promotion is complete. |
| Mismatch | Something on the destination does not match what was planned | Do not re-execute blindly. Assess with [Recovery](recovery.md). |
| Not verified | Verification has not been run | Run it. An unverified promotion is an unfinished one. |

A mismatch is information, not a failure of verification. The point of the step is to find mismatches while you are
still looking.

## Habits worth having

- Verify immediately, while the context of the change is fresh.
- Verify Staging promotions too, not only Production ones. A promotion that silently half-landed in Staging is how
  a bad plan reaches Production looking fine.
- If verification reports a mismatch, resolve it before building the next plan on top of that destination — a plan
  built from a wrong snapshot inherits the problem.

## Limitations

- Verification covers the managed schema types Environment Manager moves. It is not a general site health check.
- It confirms schema state, not editorial correctness. Schema that matches the plan may still be the wrong schema.

## Related

- [Promotion](promotion.md)
- [Recovery](recovery.md)
- [Deployments](deployments.md)
