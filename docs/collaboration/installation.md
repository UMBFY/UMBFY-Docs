# Collaboration Installation

## Requirements

| | |
| --- | --- |
| NuGet package | `UMBFY.Umbraco.Collaboration` |
| Umbraco | 17.x and 18.x (`[17.0.0,19.0.0)`) |
| SignalR hub | `/umbraco/collaborationHub` |
| Options section | `UMBFY:Collaboration` |
| Node.js | Not required — compiled assets ship in the package |
| Redis | Only for load-balanced installations |

Installing Collaboration also installs [Hub](../hub/README.md), which every UMBFY package depends on.

See [Supported Umbraco versions](../getting-started/supported-umbraco-versions.md) and
[Compatibility](../shared/compatibility.md).

## 1. Install the package

```bash
dotnet add package UMBFY.Umbraco.Collaboration
```

## 2. Restart the site

```bash
dotnet run
```

**On a single-server site that is all you need.** Presence is held in memory and SignalR is local — no Redis, no
configuration, no extra infrastructure.

## 3. Verify it works

1. Reload the Backoffice. **Team Pulse** appears in the header with a count of who is online.
2. Open it. You should see yourself listed.
3. Open a second browser session as a different user and confirm each sees the other.
4. Open the same content item in both, and confirm each shows the other's presence on that item.

If the badge sits on **Connecting…**, your proxy is probably not allowing WebSockets — see step 4.

## 4. Make sure your proxy allows WebSockets

Collaboration uses SignalR at `/umbraco/collaborationHub`. A reverse proxy that does not upgrade WebSocket
connections, or that blocks that path, leaves the badge stuck on **Connecting…**.

Check that your proxy:

- forwards `/umbraco/collaborationHub`
- allows the HTTP `Upgrade` and `Connection` headers through
- does not impose a short idle timeout on the connection

This is the single most common installation problem. See
[Troubleshooting](troubleshooting.md).

## 5. Load-balanced sites: enable distributed mode

In-memory presence only knows about its own server, so behind a load balancer each node would show a different list
of people. If you run more than one node, continue with
[Load-balanced Setup](load-balanced-setup.md).

## 6. Review the privacy switches

Some organisations do not want names and document titles visible across departments. Two switches control that, and
both default to showing the detail — see [Configuration](configuration.md#privacy).

## Verify it degrades safely

Worth proving once, because it is the reassurance you will want later: stop the hub (or block the path) and confirm
that the badge reports unavailable while **editing and publishing carry on working**. Collaboration degrades to "no
awareness", never to a blocked Backoffice.

## Upgrading

```bash
dotnet add package UMBFY.Umbraco.Collaboration --version <version>
```

Restart. On a load-balanced site, upgrade all nodes to the same version — mixed versions sharing one Redis instance
is not a supported configuration.

See [Versioning](../shared/versioning.md).

## Uninstalling

```bash
dotnet remove package UMBFY.Umbraco.Collaboration
```

Presence is ephemeral awareness data, so nothing of substance is left behind. Content and version history are
untouched — Collaboration never writes content.

## Next

- [Quick Start](quick-start.md)
- [Configuration](configuration.md)
- [Load-balanced Setup](load-balanced-setup.md)
