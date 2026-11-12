# Collaboration Configuration

All options live under `UMBFY:Collaboration`. Single-node installations need none of this — the defaults work.

## Full example

```json
{
  "UMBFY": {
    "Collaboration": {
      "Enabled": true,
      "Presence": {
        "HeartbeatInterval": "00:00:20",
        "AwayAfter": "00:01:00",
        "SessionExpiresAfter": "00:01:30",
        "CleanupInterval": "00:00:15"
      },
      "Distributed": {
        "Enabled": false,
        "ConnectionStringName": "UMBFY.Collaboration",
        "KeyPrefix": "umbfy:collaboration:"
      },
      "Privacy": {
        "ShowResourceNames": true,
        "ShowEditingState": true
      }
    }
  }
}
```

Environment-variable form uses the standard .NET double-underscore separator:

```bash
UMBFY__Collaboration__Privacy__ShowResourceNames=false
```

## `Enabled`

Default `true`. The master switch.

## Presence

`UMBFY:Collaboration:Presence` — the timing of presence itself. The defaults suit a normal Backoffice and most
teams never touch them.

| Setting | Default | Purpose |
| --- | --- | --- |
| `HeartbeatInterval` | 20 seconds | How often a connected client reports that it is still there |
| `AwayAfter` | 60 seconds | How long before an idle user is shown as away |
| `SessionExpiresAfter` | 90 seconds | How long before a silent session is dropped entirely |
| `CleanupInterval` | 15 seconds | How often expired sessions are swept |

These three durations are a chain, and the relationship between them matters more than the absolute values:
`HeartbeatInterval` < `AwayAfter` < `SessionExpiresAfter`. If you shorten the expiry below the heartbeat, healthy
users will flicker in and out of the list.

Shortening them makes presence more responsive and increases chatter; lengthening them means a user who closes
their laptop lingers in the list longer.

## Distributed

`UMBFY:Collaboration:Distributed` — Redis-backed shared presence, for load-balanced installations.

| Setting | Default | Purpose |
| --- | --- | --- |
| `Enabled` | `false` | Whether presence is shared between nodes |
| `ConnectionString` | — | The Redis connection, if given inline |
| `ConnectionStringName` | `UMBFY.Collaboration` | The named connection string to read instead |
| `KeyPrefix` | `umbfy:collaboration:` | Namespace for this installation's keys in Redis |
| `InstanceName` | — | Distinguishes this node |

Prefer `ConnectionStringName` and keep the value in `ConnectionStrings`, user secrets or an environment variable.

!!! danger "Never commit a Redis connection string"
    Use user secrets locally and environment variables or your host's secret store in deployed environments.

`KeyPrefix` matters when two installations share one Redis instance — give each its own prefix, or they will see
each other's users.

Leave `Enabled` at `false` on single-node and local development. See
[Load-balanced Setup](load-balanced-setup.md).

## Privacy

`UMBFY:Collaboration:Privacy`

| Setting | Default | Effect when `false` |
| --- | --- | --- |
| `ShowResourceNames` | `true` | You see *that* someone is editing, not *what* |
| `ShowEditingState` | `true` | Presence only — no viewing / editing / unsaved-changes detail |

Use these when teams should not see each other's work in detail — separate departments in one Backoffice, or
editorial embargo.

**Neither switch can reveal more than Umbraco's own permissions already allow.** They narrow what presence shows;
they never widen it. Resource presence is scoped to users allowed to browse the resource in the first place, and
display names never fall back to an e-mail address.

See [Presence](presence.md#privacy) and [Editing Awareness](editing-awareness.md).

## What is never exposed

By design, public presence data does not carry connection IDs, claims, e-mail addresses, IP addresses, Redis
internals, or content property values. Presence is ephemeral awareness data, not an activity history or an audit
log — do not treat it as one.

## Next

- [Load-balanced Setup](load-balanced-setup.md)
- [Presence](presence.md)
- [Troubleshooting](troubleshooting.md)
