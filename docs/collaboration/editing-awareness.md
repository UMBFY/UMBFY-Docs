# Editing Awareness

**What it does.** Tells you when someone else's work affects the item you have open, and offers you the latest
version instead of letting your save quietly overwrite theirs.

**Why and when to use it.** Because the default experience of concurrent editing is that the second save wins and
nobody finds out until a page looks wrong.

**Where to find it.** It appears on the content or media item you are working on.

**Required permissions.** Standard Umbraco permissions.

## What it surfaces

| Signal | What it means |
| --- | --- |
| Someone else is **viewing** this item | Low risk; worth knowing |
| Someone else is **editing** this item | A save is likely coming |
| Someone else has **unsaved changes** | A save is coming, based on what *they* loaded |
| The item **was saved or published** while you had it open | Your editor is now behind |

That last one is the important one. When it happens you are told, and offered **Review latest** — rather than having
your work silently overwritten, or silently overwriting theirs.

## Step-by-step

1. Open a content item.
2. Other people's presence on that item is shown while you work.
3. If somebody else saves or publishes it, you are notified.
4. Choose **Review latest** to see the current state before deciding what to do with your own changes.

## Understanding the result

**You see a warning and then nothing happens.** Correct. Editing awareness is advisory — it tells you, and leaves
the decision with you. It does not revert your editor or discard your work.

**Review latest shows changes you did not expect.** That is the feature paying for itself. Reconcile deliberately.

**You see a conflict warning for your own save.** A bug, fixed in 1.0.1 / 1.0.2. Update the package — see
[Troubleshooting](troubleshooting.md).

## It is awareness, not locking

Worth being explicit, because the expectation gap causes complaints:

- Collaboration **does not lock** content. Two people can open and edit the same item.
- It **does not replace Umbraco authorization**. Somebody who may edit an item still may.
- It **does not replace content versioning**. Umbraco's own version history remains the recovery mechanism.

What it does is remove the "I had no idea anyone else was in there" class of accident, which is the common one.

## When Collaboration is unavailable

The badge says so, and **editing and publishing carry on working**. You lose awareness, not the ability to work. A
hub outage must never stop an editor publishing — that is a deliberate design decision, not a side effect.

## Privacy

With `ShowEditingState: false`, the editing/viewing/unsaved distinction is not shown — only that somebody is
present. With `ShowResourceNames: false`, you see that somebody is editing but not what. Neither switch reveals
more than Umbraco's permissions already allow. See [Configuration](configuration.md#privacy).

## Limitations

- Advisory only — no locking, no forced reload, no automatic merge.
- Requires a live SignalR connection. No connection means no awareness.
- On a multi-node site without Redis, awareness only covers users on the same node — see
  [Load-balanced Setup](load-balanced-setup.md).

## Related features

- [Presence](presence.md)
- [Load-balanced Setup](load-balanced-setup.md)
- [Troubleshooting](troubleshooting.md)
