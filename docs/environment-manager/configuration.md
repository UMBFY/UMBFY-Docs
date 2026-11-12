# Environment Manager Configuration

All options live under the `UMBFY:EnvironmentManager` section. Configure them in `appsettings.json`, an
environment-specific override file, user secrets, or environment variables.

## Minimum configuration

```json
{
  "UMBFY": {
    "EnvironmentManager": {
      "Enabled": true,
      "LocalIdentity": "ENV-LOCAL-001",
      "LocalEnvironmentType": "Local",
      "RemoteApiKey": "<user secrets or environment variable>",
      "AllowHttpForLocalhost": true,
      "ConnectionTimeoutSeconds": 15
    }
  }
}
```

Environment-variable form uses the standard .NET double-underscore separator:

```bash
UMBFY__EnvironmentManager__LocalIdentity=ENV-PROD-001
UMBFY__EnvironmentManager__LocalEnvironmentType=Production
UMBFY__EnvironmentManager__RemoteApiKey=<secret>
```

## Options

### `Enabled`

Whether Environment Manager is active on this site.

### `LocalIdentity`

This site's identity as a **logical environment**. It must be **unique per logical environment**, and it is also
what licences are counted by.

A load-balanced site with four application nodes shares **one** `LocalIdentity` — it is one environment, not four.
Giving each node its own identity will both break promotion targeting and inflate your licensed site count.

Use something stable and readable: `ENV-PROD-001`, `acme-staging`.

### `LocalEnvironmentType`

One of:

| Value | Meaning |
| --- | --- |
| `Local` | A developer machine |
| `Development` | A shared development environment |
| `Staging` | Pre-production |
| `Production` | Live |

This is not cosmetic. `Production` is an explicit environment type that carries stronger acknowledgements before a
promotion will execute against it.

### `RemoteApiKey`

The inbound key **this** site accepts from its peers. A site that will receive a promotion must have one; a site
that only ever acts as a source does not strictly need one, but configuring it everywhere keeps environments
symmetrical.

!!! danger "Never commit this value"
    Use user secrets locally and environment variables or your host's secret store in deployed environments. An API
    key in source control is a key you have to rotate.

This is **not** your licence. See [Security](security.md#two-different-credentials).

### `AllowHttpForLocalhost`

Default behaviour requires **HTTPS** for peer communication. Setting this to `true` permits plain HTTP for
localhost only, for local development.

Leave it `false` — or omit it — in every deployed environment.

### `ConnectionTimeoutSeconds`

How long to wait for a peer before treating the call as failed. `15` is a sensible starting point. Raise it if a
geographically distant peer times out on large snapshots; do not raise it to mask a genuinely unreachable peer.

## Per-environment configuration pattern

Each environment gets its own identity and type. A typical set:

=== "Local"

    ```json
    {
      "UMBFY": {
        "EnvironmentManager": {
          "Enabled": true,
          "LocalIdentity": "ENV-LOCAL-001",
          "LocalEnvironmentType": "Local",
          "AllowHttpForLocalhost": true
        }
      }
    }
    ```

=== "Staging"

    ```json
    {
      "UMBFY": {
        "EnvironmentManager": {
          "Enabled": true,
          "LocalIdentity": "ENV-STAGING-001",
          "LocalEnvironmentType": "Staging",
          "AllowHttpForLocalhost": false
        }
      }
    }
    ```

=== "Production"

    ```json
    {
      "UMBFY": {
        "EnvironmentManager": {
          "Enabled": true,
          "LocalIdentity": "ENV-PROD-001",
          "LocalEnvironmentType": "Production",
          "AllowHttpForLocalhost": false
        }
      }
    }
    ```

In each case `RemoteApiKey` comes from secrets, not from the file.

## Identity reference

| Concern | Value |
| --- | --- |
| Options section | `UMBFY:EnvironmentManager` |
| Alias prefix | `UMBFY.EnvironmentManager.` |
| App_Plugins folder | `/App_Plugins/UMBFY.EnvironmentManager/` |
| Management API prefix | `umbfy/environment-manager` |
| Remote protocol | `/umbraco/umbfy/environment-manager/v1/*` |
| Protocol version | `1` |

## Licensing

Licence activation is done from the Backoffice rather than from configuration — see
[Editions and Licensing](editions-and-licensing.md).

## Next

- [Environments](environments.md)
- [Security](security.md)
- [Troubleshooting](troubleshooting.md)
