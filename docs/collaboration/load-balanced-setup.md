# Load-balanced Setup

**What it does.** Shares presence between nodes through Redis, so every server shows the same list of people.

**When you need it.** Any installation with more than one application node. Single-node sites and local
development need none of this.

**Why.** In-memory presence only knows about its own server. Behind a load balancer, each node would show a
different list of people — which looks like a bug and is really a missing configuration.

## 1. Configure Redis

```json
{
  "ConnectionStrings": {
    "UMBFY.Collaboration": "YOUR_REDIS_CONNECTION"
  },
  "UMBFY": {
    "Collaboration": {
      "Distributed": {
        "Enabled": true,
        "ConnectionStringName": "UMBFY.Collaboration",
        "KeyPrefix": "umbfy:collaboration:"
      }
    }
  }
}
```

!!! danger "Keep the connection string out of source control"
    Use user secrets locally and environment variables or your host's secret store in deployed environments. Never
    commit it, and never paste it into a public issue.

| Setting | Purpose |
| --- | --- |
| `Enabled` | Turns on shared presence. Must be `true` on **every** node |
| `ConnectionStringName` | The named connection string to read. Defaults to `UMBFY.Collaboration` |
| `ConnectionString` | An inline alternative, if you must |
| `KeyPrefix` | Namespace for this installation's keys. Defaults to `umbfy:collaboration:` |
| `InstanceName` | Distinguishes this node |

## 2. Apply it to every node

All nodes must have `Distributed.Enabled: true` and point at the **same** Redis instance with the **same**
`KeyPrefix`. A node left on in-memory presence will show its own private list and look broken.

Upgrade all nodes to the same package version too. Mixed versions sharing one Redis instance is not a supported
configuration.

## 3. Allow WebSockets through the load balancer

SignalR needs its connection to survive. Check that your load balancer and any reverse proxy in front of it:

- forward `/umbraco/collaborationHub`
- allow the HTTP `Upgrade` and `Connection` headers through
- do not impose a short idle timeout on the connection
- **use sticky sessions**, or allow the SignalR connection to persist to one node

A long-polling fallback across nodes without stickiness is the usual cause of a badge that connects and then drops
repeatedly.

## 4. Verify

1. Sign in as two different users, and confirm by the load balancer that they landed on **different nodes**.
2. Each should see the other in Team Pulse.
3. Open the same content item in both and confirm resource presence appears on both.
4. Close one session and confirm it drops out of the other's list within about a minute and a half — see
   [Presence](presence.md#how-presence-expires).

Step 1 is the one people skip, and it is the only one that actually proves distributed mode is working. Two sessions
that both happened to hit the same node will look correct whether Redis is configured or not.

## Sharing one Redis instance between installations

Give each installation its own `KeyPrefix`. Two installations sharing a prefix will see each other's users, which is
confusing at best and a privacy problem at worst.

## If Redis is unavailable

Collaboration degrades to no awareness; **editing and publishing carry on working**. The badge reports unavailable
rather than blocking the Backoffice.

## Diagnostics

| Symptom | Cause |
| --- | --- |
| Each server shows a different list of people | At least one node is not in distributed mode, or they point at different Redis instances or prefixes |
| Badge connects then drops repeatedly | No sticky sessions, or an idle timeout on the proxy |
| Badge stuck on **Connecting…** | WebSockets not allowed, or `/umbraco/collaborationHub` blocked |
| Unexpected users in the list | Another installation shares the same Redis instance and `KeyPrefix` |
| "Unavailable" on every node | Redis is unreachable. Editing and publishing are unaffected |

See [Troubleshooting](troubleshooting.md).

## Related

- [Configuration](configuration.md#distributed)
- [Presence](presence.md)
- [Compatibility](../shared/compatibility.md)
