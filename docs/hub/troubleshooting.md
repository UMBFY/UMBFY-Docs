# Hub Troubleshooting

## The UMBFY section does not appear

**Cause.** The section is not granted to your user group. A new Umbraco section is invisible until a group has it —
including to the user who installed the package.

**Fix.** **Users → Groups →** your group **→ Sections →** tick **UMBFY → Save**, then reload the Backoffice.

See [Installation step 3](installation.md#3-grant-the-umbfy-section-to-a-user-group).

## Everything reads "Not checked"

**Cause.** No UMBFY account is connected, so Hub has had no opportunity to check updates or licences.

**This is expected, not a fault.** Free capabilities are unaffected. Connect an account if you want update checks —
see [UMBFY Account](account.md).

## A package I installed is missing from the list

**Cause.** The package did not register itself with Hub, which means it did not start.

**Fix.**

1. Check the site started cleanly — look for startup exceptions in the Umbraco log.
2. Confirm the package's assembly actually loaded; a restore or build failure can leave a reference without an
   assembly.
3. Confirm the installed Umbraco version is within the package's supported range — see
   [Compatibility](../shared/compatibility.md).
4. Restart the site and reload the Backoffice.

Hub lists what loaded rather than what is referenced, which is why a failed package is absent rather than shown as
broken.

## Uninstalling UMBFY packages leaves Hub behind

**Cause.** Hub is a dependency of every other UMBFY package, so it cannot be removed while one of them is still
installed.

**Fix.** Remove the feature packages first and `UMBFY.Umbraco.Hub` last.

## The Backoffice logo or login screen changed after installing a package

**Cause.** Branding was enabled. It is **off** by default, so this only happens if
`UMBFY:Hub:Branding:Enabled` was set to `true`.

**Fix.** Set it back to `false`, or set your own `Umbraco:CMS:Content` image values — explicit client values always
win over UMBFY branding. See [Configuration](configuration.md#branding).

## A licence shows a problem after an outage

**Cause.** Hub could not reach the account to refresh licence state.

**Expected behaviour.** Licences are verified offline. An outage never grants paid access, and never revokes a valid
licence already in place. Once connectivity returns, the state refreshes on the next check.

## Usage statistics are not being sent

**Expected.** Statistics are off until an administrator opts in from the Backoffice, and an administrator can remove
the option entirely with `UMBFY:Hub:UsageStatistics:Allowed = false`. See
[Configuration](configuration.md#usage-statistics).

## Still stuck

Collect the Hub version, your Umbraco version and the installation id from **UMBFY → Settings → About this
installation**, then see [Reporting Issues](../shared/reporting-issues.md). Redact secrets from any log excerpt
before sharing it.
