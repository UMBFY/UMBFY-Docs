# Hub Installation

Hub is the UMBFY Backoffice section. Every other UMBFY package depends on it, so in most installations Hub arrives
automatically and this page is a verification checklist rather than a separate install.

## Requirements

| | |
| --- | --- |
| NuGet package | `UMBFY.Umbraco.Hub` |
| Umbraco | 17.x and 18.x (`[17.0.0,19.0.0)`) |
| Depends on | `UMBFY.Umbraco.Shared` `[1.1.0,2.0.0)` |
| Backoffice assets | `/App_Plugins/UMBFY.Hub/` |
| Node.js | Not required — compiled assets ship in the package |

See [Supported Umbraco versions](../getting-started/supported-umbraco-versions.md) and
[Compatibility](../shared/compatibility.md) before installing or upgrading.

## 1. Install the package

```bash
dotnet add package UMBFY.Umbraco.Hub
```

If you are installing a feature package such as Content Guard, Collaboration or Media Order, install that instead —
Hub comes with it as a dependency.

## 2. Restart the site

```bash
dotnet run
```

Hub registers its section and its package registry during startup. There is no client build step.

## 3. Grant the UMBFY section to a user group

!!! warning "This is the step most people miss"
    A new Umbraco section is not visible until it is granted to a user group. Until you do this, the **UMBFY**
    section is invisible — including to the user who installed the package.

1. Open **Users** in the Backoffice.
2. Choose **Groups**, then the group that should see UMBFY.
3. Open **Sections**.
4. Tick **UMBFY**.
5. **Save**.

Administrators usually hold all sections already. Editor and writer groups normally do not, so grant it explicitly
to any group that needs it.

## 4. Verify the installation

1. Reload the Backoffice and confirm the **UMBFY** section appears.
2. Open it. The **Dashboard** should load with health, updates and account tiles.
3. Check the installed-packages table lists every UMBFY package you expect.
4. Open **Settings → About this installation** and note the Hub version and installation id.

Time-based tiles reading **Not checked** at this point is expected — it means no UMBFY account is connected yet.
See [UMBFY Account](account.md).

## Upgrading

Hub follows [semantic versioning](../shared/versioning.md). Upgrade with the normal NuGet flow and restart:

```bash
dotnet add package UMBFY.Umbraco.Hub --version <version>
```

Because other packages declare a version range on Hub, upgrading Hub on its own is supported within the same major
version. Check each package's release notes before a major upgrade.

## Uninstalling

Uninstall feature packages first and `UMBFY.Umbraco.Hub` last, because the feature packages depend on it:

```bash
dotnet remove package UMBFY.Umbraco.Hub
```

Removing the package removes the section. Stored Hub state is not deleted by the package removal itself.

## Next

- [Quick Start](quick-start.md) — read the dashboard and clear what needs attention
- [Configuration](configuration.md) — branding, public reports, usage statistics
- [Troubleshooting](troubleshooting.md)
