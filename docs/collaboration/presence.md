# Presence

**What it does.** Shows which Backoffice users are online, and who is on the same content or media item as you.

**Why and when to use it.** Continuously — it is ambient. The value is finding out somebody else is in a document
*before* you both start editing it.

**Where to find it.** **Team Pulse**, the presence control in the Backoffice header, and inline on content and
media items.

**Required permissions.** Standard Umbraco permissions. Resource presence is scoped to users allowed to browse the
resource.

## Two kinds of presence

| Kind | What it answers |
| --- | --- |
| **Online presence** | Who is in the Backoffice right now |
| **Resource presence** | Who else is on *this* content or media item |

Team Pulse carries the first with a count in the header. The second appears while you work on an item.

## Step-by-step

1. Open **Team Pulse** in the Backoffice header.
2. Read who is online, what they are on, and their state — viewing, editing, or unsaved changes.
3. Open a content item. Other people on the same item are shown inline while you work.
4. Act on it: if somebody is already editing, talk to them rather than racing them.

## States

| State | Meaning |
| --- | --- |
| **Viewing** | The item is open, no changes made |
| **Editing** | Changes are being made |
| **Unsaved changes** | There is work in the editor that has not been saved |
| **Away** | Idle beyond `AwayAfter` (60 seconds by default) |

"Unsaved changes" is the one to respect. It means a save is coming, and that save will be based on what the other
person loaded.

## How presence expires

A connected client heartbeats every `HeartbeatInterval` (20 seconds). Silence for `AwayAfter` shows the user as
away; silence for `SessionExpiresAfter` (90 seconds) drops the session. Expired sessions are swept every
`CleanupInterval`.

The practical consequence: somebody who closes their laptop lid disappears from the list within about a minute and a
half, not instantly. Tunable — see [Configuration](configuration.md#presence).

## Privacy

Two switches narrow what presence shows:

- `ShowResourceNames: false` — you see *that* someone is editing, not *what*.
- `ShowEditingState: false` — presence only, no viewing / editing / unsaved detail.

**Neither can reveal more than Umbraco's permissions already allow.** Resource presence is scoped to users allowed
to browse the resource, client-supplied identity is not trusted as authority, and display names never fall back to
an e-mail address.

See [Configuration](configuration.md#privacy).

## Understanding the result

A list showing your colleagues is the normal state. Two results deserve interpretation:

**"Unavailable".** The SignalR transport is disconnected. Editing and publishing still work — Collaboration degrades
to no awareness, never to a blocked Backoffice. See [Troubleshooting](troubleshooting.md).

**Each server shows a different list.** A multi-node installation without Redis. Each node only knows its own
users. See [Load-balanced Setup](load-balanced-setup.md).

## Limitations

- Presence is **ephemeral awareness data**, not an activity log or an audit trail. It is not retained and should not
  be used to answer "who edited what last week" — Umbraco's own versioning does that.
- It is awareness, not locking. Presence does not prevent two people editing the same item; see
  [Editing Awareness](editing-awareness.md) for what happens when they do.
- Public presence data never carries connection IDs, claims, e-mail addresses, IP addresses, Redis internals or
  content property values.

## Related features

- [Editing Awareness](editing-awareness.md)
- [Load-balanced Setup](load-balanced-setup.md)
- [Configuration](configuration.md)
