# Editions and Licensing

## Editions

| Edition | Includes |
| --- | --- |
| **Free** | Dashboard, connection diagnostics, snapshots, compare, basic drift — **no Hub and no licence required** |
| **Professional** | Free, plus promotion plan and execute, bootstrap, verification, recovery, multi-environment, advanced cluster and advanced approvals |
| **Agency** | Professional, plus advanced governance |
| **Enterprise** | Agency, plus enterprise integration hooks |

Everything in the Free edition works without [Hub](../hub/README.md) and without a licence. You can register
environments, prove connectivity, snapshot, compare and see basic drift on an unlicensed site — which is enough to
decide whether the package earns its place before you pay for it.

Paid capabilities require a valid signed licence, or a usable Hub-reported licence mapped to an edition.

## Activating a licence

**Required permissions.** Backoffice **administrator**.

1. Open **Environment Manager → Settings**.
2. Paste the signed licence envelope JSON.
3. Activate.
4. Confirm the reported edition and granted capabilities.

## Offline behaviour

Licences are **RS256 signed and verified offline**. Once a valid licence is activated it keeps working offline
until it expires.

Two consequences, both deliberate:

- A Hub or network outage **never revokes** a valid activated licence.
- A Hub or network outage **never grants** paid access. Unavailability is not an entitlement.

Clearing the licence returns the site to the Free edition. Nothing is destroyed by doing so; the paid capabilities
simply stop being offered.

## How sites are counted

Licences count **logical environments**, identified by `LocalIdentity` — not application nodes.

A load-balanced Production site with four servers behind it is **one** environment, not four, because all four
nodes share one `LocalIdentity`. Giving each node its own identity would both break promotion targeting and inflate
your count.

A typical four-environment chain — Local, Development, Staging, Production — is four logical environments
regardless of how many servers sits behind each.

## Licence credentials are not environment credentials

This is the single most common confusion, so it is worth being blunt about:

| Credential | What it is for | Where it lives |
| --- | --- | --- |
| **Signed licence** (or Hub-reported licence) | Which *product features* you may use | Activated in the Backoffice |
| **Environment API key** (`RemoteApiKey`) | Authenticating calls *between your own Umbraco sites* | Secrets / environment variables |

They are never interchangeable:

- Activating a licence does **not** configure or grant remote access.
- Rotating an API key does **not** change your entitlements.

See [Security](security.md).

## Checking your current state

**Environment Manager → Settings** reports the active edition and the capabilities it grants. If a paid action is
refused, check there first — the usual answer is that the site is on Free, or the licence is not usable.

## Test keys

The repository's test signing key is **never** trusted in a Production environment. An "unknown license signing key
id" error on Production means a test licence was deployed where a real one is required.

## Related

- [Configuration](configuration.md)
- [Security](security.md)
- [Hub](../hub/README.md)
- [Troubleshooting](troubleshooting.md)
