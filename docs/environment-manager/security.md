# Security

Environment Manager mutates schema on real environments and talks to other sites over the network. Both of those
deserve to be set up deliberately.

## Two different credentials

| Credential | What it is for | Where it lives |
| --- | --- | --- |
| **Signed licence** (or Hub-reported licence) | Which *product features* you may use | Activated in the Backoffice |
| **Environment API key** (`RemoteApiKey`) | Authenticating Environment Manager calls *between your own Umbraco sites* | Secrets / environment variables |

Activating a licence does not grant remote access. Rotating an API key does not change your entitlements. See
[Editions and Licensing](editions-and-licensing.md).

## API keys

`RemoteApiKey` is the **inbound** key a site accepts from its peers. When you register a peer, you supply the key
*that peer* accepts.

!!! danger "Never commit an API key"
    Use user secrets locally and environment variables or your host's secret store in deployed environments. An API
    key in source control is a key you have to rotate.

Practical rules:

- Give each environment its own key. A single shared key means one leak compromises the whole chain.
- Rotate the destination's key and update it on every peer that registered that destination.
- A site that only ever acts as a source does not strictly need an inbound key, though configuring one everywhere
  keeps environments symmetrical.

## Transport

Peer communication requires **HTTPS**. The only exception is `AllowHttpForLocalhost`, which permits plain HTTP for
localhost only, for local development.

Leave `AllowHttpForLocalhost` at `false` — or omit it — in every deployed environment. Enabling it in a deployed
environment does not make a remote peer reachable over HTTP; it weakens a local-development allowance in a place
where you do not want one.

## Mutation is deny-by-default

There is one path by which schema changes:

```text
Compare → Plan → Approve → Execute → Verify → (Recover)
```

No step can be skipped, and each is recorded. The plan's fingerprint is bound to its contents, so an approval
applies to the exact plan that was approved and an altered plan cannot be executed under it.

`Production` is an explicit environment type carrying stronger acknowledgements. Do not mislabel a Production
environment as Staging to avoid the friction — the label is what the extra control hangs off.

## Permissions

- The Environment Manager section is granted through standard Umbraco user-group section security. Grant it
  deliberately; schema promotion is an operations task, not an editorial one.
- Licence activation requires a Backoffice **administrator**.
- Plan approval is a recorded act, attributable to whoever performed it.

## The audit trail

For every run, [Deployments](deployments.md) holds the plan and its fingerprint, the approval, the execution and its
outcome, the verification result, and any recovery. That set is what lets you account for a schema change after the
fact. A promotion without verification is a change you cannot fully account for.

## Reporting a security issue

Do not open a public issue for a suspected vulnerability. Follow
[SECURITY.md](https://github.com/UMBFY/UMBFY-Packages/blob/main/SECURITY.md).

When reporting any ordinary bug, never include API keys, licence keys or connection strings — redact log excerpts
first. See [Reporting Issues](../shared/reporting-issues.md).

## Related

- [Configuration](configuration.md)
- [Environments](environments.md)
- [Editions and Licensing](editions-and-licensing.md)
