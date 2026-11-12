# Collaboration Quick Start

Five minutes, and it needs two people — or two browser sessions signed in as different Backoffice users, which is
easier to arrange.

**Before you start:** the package installed and the site restarted. See [Installation](installation.md).

## 1. Find Team Pulse

Reload the Backoffice. **Team Pulse** is the presence control in the Backoffice header, showing a count of who is
online.

Open it. You see who is here, what they are on, and whether they are viewing, editing, or have unsaved changes.

## 2. Prove it with a second user

Sign in as a different user in a second browser session.

Each should now see the other in Team Pulse. If not, and the badge reads **Connecting…**, the SignalR hub is not
reachable — check that your proxy allows WebSockets on `/umbraco/collaborationHub`.

## 3. Open the same item in both

Open one content item in both sessions.

Each session now shows the other person's presence **on that item**, and whether they are viewing or editing. That
is the core of the feature: you find out somebody else is in there *before* you both start typing.

[More on Presence →](presence.md)

## 4. Trigger a real conflict warning

In the second session, make a change and **save**.

The first session is told that the item changed underneath it, and offered **Review latest** — rather than having
its work silently overwritten on the next save.

That is editing awareness working. [More on Editing Awareness →](editing-awareness.md)

## 5. Confirm it fails soft

Worth doing once so you trust it later. Stop the site's hub connection — block `/umbraco/collaborationHub` at your
proxy, or simply go offline.

The badge reports that Collaboration is unavailable, and **editing and publishing keep working**. It degrades to
"no awareness", never to a blocked Backoffice.

## 6. Decide your privacy level

Two switches, both defaulting to showing the detail:

| Setting | Set to `false` to... |
| --- | --- |
| `ShowResourceNames` | show *that* someone is editing, not *what* |
| `ShowEditingState` | show presence only — no viewing / editing / unsaved detail |

Neither switch can reveal more than Umbraco's own permissions already allow. See
[Configuration](configuration.md#privacy).

## 7. If you run more than one server

Stop here and read [Load-balanced Setup](load-balanced-setup.md). In-memory presence only knows about its own node,
so without Redis each server shows a different list of people — which looks like a bug and is really a
configuration gap.

## Next

- [Presence](presence.md) · [Editing Awareness](editing-awareness.md)
- [Configuration](configuration.md)
- [FAQ](faq.md)
