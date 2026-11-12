# Hub Packages

**What it does.** Lists every installed UMBFY package with its status, version, update availability, licence state
and a link to its documentation.

**When to use it.** After installing or upgrading a package, when a licence question comes up, or when the dashboard
tells you something needs attention.

**Where to find it.** **UMBFY → Packages**.

**Required permissions.** The UMBFY section must be granted to your user group.

## What a package card shows

| Field | Meaning |
| --- | --- |
| **Status** | What the package itself reports: healthy, warning or error |
| **Version** | The version currently installed |
| **Update** | Whether a newer version is available (requires a connected account) |
| **Licence** | The package's licence state, where the package is licensed |
| **Documentation** | A link to that package's documentation |

Packages with problems sort to the top, so the first card is always the one worth reading.

## Step-by-step: confirm a package installed correctly

1. Open **UMBFY → Packages**.
2. Find the package you just installed.
3. Confirm the version matches what you installed.
4. Confirm the status is healthy.
5. If the package is licensed, confirm the licence state is what you expect.

## Understanding the result

- **Healthy, no update, no licence problem** — nothing to do.
- **Update available** — see that package's release notes before upgrading, then upgrade through NuGet and restart.
- **Licence problem** — the package falls back to its free capabilities. Check the licence in that package's own
  settings; a Hub outage never grants paid access.
- **Package missing from the list** — it did not register. See [Troubleshooting](troubleshooting.md).

## Package registration

Packages are not hard-coded into Hub. Each one registers itself against the shared package registry during startup,
which is why the list reflects what actually loaded rather than what is referenced in your project file. A package
that failed to start is absent rather than shown as broken.

## Limitations

- Update availability requires a connected UMBFY account. Without one, the update column reads **Not checked**.
- Hub lists UMBFY packages only. Third-party or Umbraco core packages are not shown here.

## Related

- [Dashboard](dashboard.md)
- [UMBFY Account](account.md)
- [Versioning](../shared/versioning.md)
