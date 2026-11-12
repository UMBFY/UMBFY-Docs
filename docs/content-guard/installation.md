# Content Guard Installation

## Requirements

| | |
| --- | --- |
| NuGet package | `UMBFY.Umbraco.ContentGuard` |
| Umbraco | 17.x and 18.x (`[17.0.0,19.0.0)`) |
| Backoffice assets | `/App_Plugins/UMBFY.ContentGuard/` |
| Options section | `UMBFY:ContentGuard` |
| Node.js | Not required — compiled assets ship in the package |

Installing Content Guard also installs [Hub](../hub/README.md), which every UMBFY package depends on.

See [Supported Umbraco versions](../getting-started/supported-umbraco-versions.md) and
[Compatibility](../shared/compatibility.md) before installing or upgrading.

## 1. Install the package

```bash
dotnet add package UMBFY.Umbraco.ContentGuard
```

## 2. Restart so the migration runs

```bash
dotnet run
```

The package migration creates the dependency-index tables on first start. Let the site finish starting.

## 3. Let the first index build finish

On a site that already has content, Content Guard bootstraps its dependency index **automatically**.

!!! tip "You do not need to re-save anything"
    Existing content and media are indexed for you. On a large site the first build takes a few minutes.

While it builds, [Content Health](content-health.md) reports **Initializing** or **Rebuilding**, and the guards
**fail closed** — they will not claim an item is safe to delete on the strength of a half-built index.

| Index state | What it means |
| --- | --- |
| **Initializing** / **Rebuilding** | Not trustworthy yet. Guards stay cautious |
| **Ready** | Normal operation |
| **Unhealthy** / **Failed** | Something went wrong; the last error is recorded. Guards stay cautious |

## 4. Grant the UMBFY section (optional but recommended)

Content Guard's own views appear on content and media items, so they need no extra section grant. The
[Content Health](content-health.md) dashboard and the Hub views do live in a section — grant it to the groups that
need it:

**Users → Groups →** the group **→ Sections →** tick the section **→ Save**.

## 5. Verify the installation

1. Open [Content Health](content-health.md) and wait for the index state to reach **Ready**.
2. Open any content item that you know references an image.
3. Open that image in Media and switch to **Where Used** — the content item should be listed, with the property it
   came from.
4. If you are on Professional or above, check that **Impact** appears on the item too.

If Where Used is empty for something you know is linked, the reference probably comes from a property editor with no
scanner — see [Configuration](configuration.md#custom-property-editors).

## 6. Choose your policies

Defaults are production-safe (`RequireConfirmation` for both guards). Review
[Configuration](configuration.md) if you want a different editorial policy, and read
[Safe Delete](safe-delete.md#before-you-choose-block) before setting anything to `Block`.

## Upgrading

```bash
dotnet add package UMBFY.Umbraco.ContentGuard --version <version>
```

Restart so any new migration runs. Check the release notes first, and see
[Versioning](../shared/versioning.md).

## Uninstalling

```bash
dotnet remove package UMBFY.Umbraco.ContentGuard
```

Removing the package removes the guards and the views. Content is untouched — Content Guard never modifies content,
it only reads it and reports.

Uninstall `UMBFY.Umbraco.Hub` last, if you are removing UMBFY packages entirely.

## Next

- [Quick Start](quick-start.md)
- [Configuration](configuration.md)
- [Editions](editions.md)
