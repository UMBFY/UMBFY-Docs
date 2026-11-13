# Environment Manager Quick Start

This runs one real schema promotion from a local site to a development site. Do it in that direction first —
not into Staging, and certainly not into Production.

**Before you start:** the package installed and configured on **both** sites, and the Environment Manager section
granted to your user group. See [Installation](installation.md) and [Configuration](configuration.md).

## 1. Confirm each site knows who it is

On each site, open **Environment Manager → Overview** and confirm it reports the `LocalIdentity` and
`LocalEnvironmentType` you configured. A site that reports the wrong identity will be targeted wrongly later.

## 2. Register the peer

On the source site:

1. **Environment Manager → Environments → Add**.
2. Enter the destination's URL and its identity.
3. Supply the API key the destination accepts — that is the destination's `RemoteApiKey`.
4. Save.

A setup wizard walks you through this the first time.

## 3. Test the connection

Choose **Test connection** for the peer you just added.

Nothing can be promoted until connectivity is proven. If this fails, stop here and fix it —
[Troubleshooting](troubleshooting.md) lists the three usual causes.

## 4. Compare

**Compare**, choosing the source and the destination. Environment Manager takes a schema snapshot of each and shows
you the differences — Document Types, Element Types, Data Types, Templates, Dictionary items and Languages.

Read the differences before selecting anything. Dependency mapping shows what a given change pulls in with it, so
a single Document Type may legitimately bring a Data Type along.

[More on comparing and drift &rarr;](compare-and-drift.md)

## 5. Plan

Select the differences you want to promote and build a **plan**.

The plan is **immutable**. Its fingerprint is bound, which is what makes the approval in the next step meaningful:
an altered plan cannot be executed under an old approval.

## 6. Approve

Approve the plan.

This is a deliberate gate, not a formality. On a real team the approver is not always the planner, and the approval
is recorded against the plan.

## 7. Execute

Execute the approved plan against the destination.

Progress is live. **Deployments** shows the run while it is going and keeps it in history afterwards.

## 8. Verify

Run **verification**. This independently re-reads the destination and confirms it matches what the plan said it
would do — rather than trusting the executor's own report that it succeeded.

Verification is the step people skip and then regret. Treat a promotion as incomplete until it has verified.

[More on verification &rarr;](verification.md)

## 9. If something went wrong

Use **Recovery** to assess and then execute recovery for supported managed schema. Assess first; recovery is itself
a schema mutation and goes through the same controls.

[More on recovery &rarr;](recovery.md)

## What you just used

Steps 1&ndash;4 are **Free** edition capabilities. Steps 5&ndash;9 — plan, approve, execute, verify, recover — are
**Professional** and above. If a paid action is refused, check your edition under
[Editions and Licensing](editions-and-licensing.md).

## Next

- [Promotion](promotion.md) — the full flow in detail, including Production acknowledgements
- [Deployments](deployments.md) — history, filters and live progress
- [Bootstrap](bootstrap.md) — for a near-empty destination, instead of difference-by-difference promotion
