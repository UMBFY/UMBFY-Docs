# Environment Manager Troubleshooting

## Test connection fails

Three usual causes, in order of likelihood:

1. **Wrong API key.** The key you supply when registering a peer must be the key *that peer* accepts — its own
   `RemoteApiKey`. Supplying the source's key is the classic mistake.
2. **HTTP without the allowance.** Peer communication requires HTTPS. Plain HTTP is permitted only for localhost,
   and only when `AllowHttpForLocalhost` is `true` on that peer.
3. **The peer is unreachable.** Firewall, private network, the site is not running, or the package is not installed
   there.

Also check that both ends run the same package version, and that `ConnectionTimeoutSeconds` is not simply too low
for a distant peer with a large schema.

## "Unknown license signing key id" on Production

**Cause.** A repository *test* signing key is never trusted in a Production environment.

**Fix.** Deploy a real signed licence. See [Editions and Licensing](editions-and-licensing.md).

## A paid action is refused

**Cause.** The site is on the **Free** edition, or there is no usable licence.

**Fix.** Open **Environment Manager → Settings** and check the reported edition and granted capabilities. Remember
that a Hub outage never grants paid access — if Hub is unreachable and the site has no activated signed licence, it
is on Free, correctly.

Free covers dashboard, connection diagnostics, snapshots, compare and basic drift. Plan, execute, bootstrap,
verify and recover are Professional and above.

## The plan will not execute

Two causes:

1. **It has not been approved.** Approval is a required gate, not a formality.
2. **The schema moved underneath it.** A plan is built from a specific snapshot pair and its fingerprint is bound to
   its contents. If either environment changed, the plan no longer describes reality.

**Fix.** Re-compare and build a new plan. Do not look for a way to force an old plan through — the fingerprint
check is what makes the audit trail trustworthy.

## Execution failed partway

1. Open the deployment record and read how far it got.
2. Run a [recovery](recovery.md) **assessment** before doing anything else.
3. Execute recovery if the assessment describes what you want.
4. Re-run [verification](verification.md).

Do not re-execute the original plan as a fix. Compare again and plan from the destination's real current state.

## Verification reports a mismatch

This is verification doing its job. Something on the destination does not match what was planned.

Assess with [recovery](recovery.md) rather than re-executing. Resolve the mismatch before building another plan on
top of that destination, or the next plan inherits the problem.

## Two environments behave as one

**Cause.** They share a `LocalIdentity`. Identity must be unique per **logical** environment.

**Fix.** Give each logical environment its own identity, then re-register it on the peers that had registered it.
Note the inverse mistake too: all nodes of one load-balanced site must **share** one identity.

## Nodes of a load-balanced site each count as a site

**Cause.** Each node was given its own `LocalIdentity`.

**Fix.** All nodes of one logical environment share one identity. That also fixes promotion targeting, which the
split identities would have broken.

## The Environment Manager section does not appear

**Cause.** The section is not granted to your user group.

**Fix.** **Users → Groups →** your group **→ Sections →** tick **Environment Manager → Save**, then reload the
Backoffice.

## Comparison times out

**Cause.** A large schema over a slow link.

**Fix.** Raise `ConnectionTimeoutSeconds` — see
[Configuration](configuration.md#connectiontimeoutseconds). Do not raise it to mask a peer that is genuinely
unreachable; a failed connection test is a different problem.

## Still stuck

Collect the package version, your Umbraco version, the environment types involved and the deployment record id,
then see [Reporting Issues](../shared/reporting-issues.md) and [Diagnostics](../shared/diagnostics.md).

Never include API keys, licence keys or connection strings in a public issue.
