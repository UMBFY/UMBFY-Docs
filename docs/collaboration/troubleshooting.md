# Collaboration Troubleshooting

## Badge stuck on "Connecting…"

**Cause.** The SignalR hub at `/umbraco/collaborationHub` is not reachable. This is the most common installation
problem by a wide margin.

**Fix.** Check that your reverse proxy or load balancer:

- forwards `/umbraco/collaborationHub`
- allows the HTTP `Upgrade` and `Connection` headers through, so the WebSocket upgrade succeeds
- does not impose a short idle timeout on the connection

## Badge says "Unavailable"

**Cause.** The transport is disconnected — a network drop, a hub restart, or Redis unreachable on a distributed
installation.

**Expected behaviour.** **Editing and publishing still work.** Collaboration degrades to no awareness, never to a
blocked Backoffice. A hub outage must never stop an editor publishing.

If it persists, work through the "Connecting…" checks above.

## Each server shows a different list of people

**Cause.** A multi-node installation without shared presence. In-memory presence only knows about its own node.

**Fix.** Enable distributed mode on **every** node, pointing at the same Redis instance with the same `KeyPrefix` —
see [Load-balanced Setup](load-balanced-setup.md). One node left on in-memory presence is enough to produce this.

## Badge connects, then drops, repeatedly

**Cause.** On a load-balanced site, usually no sticky sessions — the connection is being handed to a different node
— or a short idle timeout on the proxy.

**Fix.** Enable sticky sessions, or allow the SignalR connection to persist to one node, and raise the idle timeout.

## Unexpected people in the list

**Cause.** Two installations share one Redis instance **and** the same `KeyPrefix`, so they see each other's users.

**Fix.** Give each installation its own `KeyPrefix`.

## You see a conflict warning for your own save

**Cause.** A bug in an early version.

**Fix.** Fixed in **1.0.1 / 1.0.2** — update the package.

## Healthy users flicker in and out of the list

**Cause.** The presence timings have been changed into an inconsistent chain. `HeartbeatInterval` must be shorter
than `AwayAfter`, which must be shorter than `SessionExpiresAfter`. If expiry is shorter than the heartbeat,
connected users are dropped before they next report in.

**Fix.** Restore the defaults (20s / 60s / 90s) or keep the ordering — see
[Configuration](configuration.md#presence).

## Somebody who left is still shown

**Expected, briefly.** A closed browser is detected by silence, not by notification. The session shows as away after
`AwayAfter` (60 seconds) and is dropped after `SessionExpiresAfter` (90 seconds), with cleanup sweeping every 15
seconds. Roughly a minute and a half, not instant.

## Names or document titles are not shown

**Cause.** A privacy switch, not a fault. `ShowResourceNames: false` hides *what* is being edited;
`ShowEditingState: false` hides the viewing/editing/unsaved distinction.

See [Configuration](configuration.md#privacy).

## An editor cannot see presence on an item

**Expected.** Resource presence is scoped to users allowed to browse the resource. Collaboration never widens what
Umbraco's permissions allow.

## Presence will not tell me who edited something last week

**By design.** Presence is ephemeral awareness data, not an activity history or an audit log, and it is not
retained. Use Umbraco's own content versioning for that question.

## Still stuck

Collect the Collaboration version, your Umbraco version, whether the installation is single- or multi-node, and
whether distributed mode is enabled, then see [Reporting Issues](../shared/reporting-issues.md) and
[Diagnostics](../shared/diagnostics.md).

!!! danger "Never post a Redis connection string"
    Redact it from any configuration excerpt before sharing. The same goes for credentials, API keys and licence
    keys.
