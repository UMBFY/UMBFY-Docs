# Collaboration FAQ

**Do I need Redis?**
Only if you run more than one application node. Single-server sites and local development use in-memory presence and
need no extra infrastructure at all.

**What happens on a multi-node site without Redis?**
Each node shows only its own users, so people see different lists. It looks like a bug and is really a missing
configuration — see [Load-balanced Setup](load-balanced-setup.md).

**Does it lock content while someone is editing?**
No. Collaboration provides **awareness**, not locking. Two people can still open the same item; the difference is
that they know about each other, and the second one to save is told rather than silently winning.

**Does it replace Umbraco permissions or versioning?**
No, and it is not meant to. Backoffice authorization remains authoritative, and Umbraco's own version history
remains the recovery mechanism.

**If the hub goes down, can my editors still work?**
Yes. Editing and publishing carry on working; the badge reports unavailable. It degrades to no awareness, never to a
blocked Backoffice.

**Why is the badge stuck on "Connecting…"?**
Almost always a proxy that does not allow the WebSocket upgrade, or one blocking
`/umbraco/collaborationHub`. See [Troubleshooting](troubleshooting.md).

**Why does someone who closed their browser still show as online?**
Because a closed browser is detected by silence. They show as away after 60 seconds and are dropped after 90. Both
are configurable.

**Can I hide what people are working on?**
Yes. `ShowResourceNames: false` shows *that* someone is editing without showing *what*, and
`ShowEditingState: false` reduces it to bare presence. Neither switch can reveal more than Umbraco's permissions
already allow.

**Can an editor see presence on content they're not allowed to see?**
No. Resource presence is scoped to users allowed to browse the resource.

**Is presence an audit log?**
No. It is ephemeral awareness data and is not retained. It will not tell you who edited what last week — content
versioning does that.

**What data is exposed about users?**
Privacy-aware display information only. Public presence data never carries connection IDs, claims, e-mail addresses,
IP addresses, Redis internals or content property values, and display names never fall back to an e-mail address.

**I get a conflict warning for my own save.**
A bug fixed in 1.0.1 / 1.0.2. Update the package.

**Do I need Node.js to install it?**
No. Compiled Backoffice assets ship in the package.

**Can I share one Redis instance between two Umbraco installations?**
Yes, but give each its own `KeyPrefix` or they will see each other's users.

**Which Umbraco versions are supported?**
17.x and 18.x (`[17.0.0,19.0.0)`). See
[Supported Umbraco versions](../getting-started/supported-umbraco-versions.md).

**Where do I report a bug?**
The [UMBFY Packages issue tracker](https://github.com/UMBFY/UMBFY-Packages/issues). Never include a Redis
connection string or any other secret.
