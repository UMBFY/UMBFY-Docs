# Environment Manager Installation

## Requirements

| | |
| --- | --- |
| NuGet package | `UMBFY.Umbraco.EnvironmentManager` |
| Current version | `1.0.0-rc.1` (release candidate) |
| Umbraco | 17.x and 18.x (`[17.0.0,19.0.0)`) |
| Backoffice assets | `/App_Plugins/UMBFY.EnvironmentManager/` |
| Options section | `UMBFY:EnvironmentManager` |
| Node.js | Not required |

!!! warning "Release candidate"
    `1.0.0-rc.1` is not published to nuget.org. It mutates schema on real environments — install it between Local
    and Development first.

## 1. Install on every environment

```bash
dotnet add package UMBFY.Umbraco.EnvironmentManager --version 1.0.0-rc.1
```

Install it on **both ends** of any promotion — the source environment and the destination environment. An
environment without the package cannot take part in a comparison or receive a promotion.

## 2. Restart so migrations run

```bash
dotnet run
```

Package migrations create the Environment Manager storage on first start. Let the site finish starting before using
the section.

## 3. Configure each site's identity

Every site needs its own identity, and any site that will *receive* a promotion needs an inbound API key. The
minimum configuration is:

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

!!! danger "Never commit `RemoteApiKey`"
    Use user secrets, environment variables or your host's secret store. The value in the snippet above is a
    placeholder.

See [Configuration](configuration.md) for every option and its default.

## 4. Grant the section to a user group

Environment Manager installs its own Backoffice section. Like any Umbraco section it is invisible until granted:

**Users → Groups →** the group **→ Sections →** tick **Environment Manager → Save**.

Schema promotion is an operations task. Grant this section deliberately rather than to every editor group.

## 5. Verify the installation

1. Reload the Backoffice and open **Environment Manager**.
2. The dashboard should load and report this site's own identity and environment type.
3. Confirm the identity matches the `LocalIdentity` you configured.
4. Run the connection diagnostics for this site.

At this point you have the Free edition working: dashboard, connection diagnostics, snapshots, compare and basic
drift. No Hub and no licence are required for any of that.

## 6. Register your peers

Continue with [Environments](environments.md) to register the other environments and prove connectivity. Nothing
can be promoted until connectivity is proven.

## Upgrading

Follow the normal NuGet flow and restart so migrations run:

```bash
dotnet add package UMBFY.Umbraco.EnvironmentManager --version <version>
```

Upgrade **all** environments in a promotion chain to the same version before using them together. Mixed versions
across a chain are not a supported configuration.

Check the release notes before upgrading, and see [Versioning](../shared/versioning.md).

## Uninstalling

```bash
dotnet remove package UMBFY.Umbraco.EnvironmentManager
```

Removing the package removes the section. Schema that has already been promoted stays in place — it is ordinary
Umbraco schema. Deployment history is not deleted by removing the package.

## Next

- [Configuration](configuration.md)
- [Quick Start](quick-start.md)
- [Security](security.md)
