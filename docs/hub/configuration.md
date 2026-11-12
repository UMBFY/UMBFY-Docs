# Hub Configuration

Every Hub setting is optional and the defaults are safe for production. Configure them in `appsettings.json`, an
environment-specific override, or environment variables.

```json
{
  "UMBFY": {
    "Hub": {
      "Branding": { "Enabled": false },
      "PublicReports": { "Enabled": true },
      "UsageStatistics": { "Allowed": true }
    }
  }
}
```

Environment-variable form uses the standard .NET double-underscore separator:

```bash
UMBFY__Hub__Branding__Enabled=true
```

## Branding

`UMBFY:Hub:Branding:Enabled` — default **`false`**.

When enabled, Hub applies UMBFY branding to the Umbraco **login screen** and the Backoffice header. It is off by
default so that installing a UMBFY package never rebrands a site on its own.

Branding fills only the `Umbraco:CMS:Content` image settings that are still at Umbraco's own default value, so a
client's own branding always wins:

```json
{
  "Umbraco": {
    "CMS": {
      "Content": {
        "BackOfficeLogo": "../media/client/logo-white.svg"
      }
    }
  }
}
```

!!! warning "Think before enabling this on a client site"
    The Umbraco login screen is a public, unauthenticated page. Enabling branding puts your supplier's mark in front
    of anyone who can reach `/umbraco`.

## Public reports

`UMBFY:Hub:PublicReports:Enabled` — default **`true`**.

On an installation that is **not** connected to a UMBFY account, this lets an editor tick *Also send this report to
UMBFY* on an individual support report, so a bug can be reported without connecting the site first.

- The option is off per report by default — somebody has to choose it each time.
- No domain, credentials or content is sent.
- Set this to `false` to remove the option entirely.

See [Support and Feedback](support-and-feedback.md).

## Usage statistics

`UMBFY:Hub:UsageStatistics:Allowed` — default **`true`**.

This setting controls whether the *option* exists at all. Statistics are **off** until an administrator explicitly
opts in from the Backoffice, and the Settings page shows the exact JSON that would be sent before you agree to it.

Set it to `false` to remove the option from the Backoffice, so no administrator on this installation can turn
statistics on.

## Per-package settings

Hub does not own other packages' configuration. Open **UMBFY → Settings** for the list of installed packages that
expose settings, each with an **Open settings** action.

For the configuration of a specific package, see that package's own documentation:

- [Content Guard configuration](../content-guard/configuration.md)
- [Collaboration configuration](../collaboration/configuration.md)
- [Media Order configuration](../media-order/configuration.md)
- [Environment Manager configuration](../environment-manager/configuration.md)

## Permissions

Access to the UMBFY section is standard Umbraco user-group section security — see
[Installation step 3](installation.md#3-grant-the-umbfy-section-to-a-user-group).

Administrative actions inside Hub, including connecting an account and opting in to usage statistics, require a
Backoffice administrator.

## Next

- [UMBFY Account](account.md)
- [Troubleshooting](troubleshooting.md)
