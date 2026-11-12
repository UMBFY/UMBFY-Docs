# UMBFY Account

**What it does.** Connects this Umbraco installation to a UMBFY account so Hub can sync licences, check for package
updates and keep your support history.

**When to use it.** When you buy a licensed package, or when you want update notifications. Free capabilities do not
need it.

**Where to find it.** **UMBFY → Dashboard → Connect UMBFY Account**.

**Required permissions.** Backoffice administrator.

## Hub works without an account

Until an account is connected:

- nothing is sent anywhere
- every free capability of every installed package keeps working
- Hub cannot tell you about updates or licences, so time-based tiles read **Not checked**

**Not checked** is therefore the correct state for an unconnected installation, not a fault.

## What connecting enables

| Capability | Without an account | With an account |
| --- | --- | --- |
| Free package features | Work | Work |
| Licence sync for paid features | Manual, per package | Synced by Hub |
| Update checks | Not checked | Checked |
| Support history in the Backoffice | Per-report only | Kept with your account |

## Step-by-step: connect

1. Sign in to the Backoffice as an administrator.
2. Open **UMBFY → Dashboard**.
3. Choose **Connect UMBFY Account**.
4. Complete the registration flow.
5. Return to the dashboard and confirm the **Account** tile reads connected.
6. Open [Packages](packages.md) and confirm update and licence columns are now populated.

## Installations and identity

A connected installation has an **installation id**, visible under **UMBFY → Settings → About this installation**.
Quote it when raising a support issue — it is how a report is tied to the right installation without you sharing
hostnames or credentials.

## Licences

Hub reports and caches licence state; it does not replace a package's own licence handling. Licences are verified
offline, so a connected account is a convenience rather than a runtime dependency:

- a Hub or network outage never grants paid access
- a Hub or network outage never revokes a valid licence that is already in place
- clearing a licence returns that package to its free capabilities

For a package that accepts a signed licence directly, see that package's documentation — for example
[Environment Manager editions and licensing](../environment-manager/editions-and-licensing.md).

## Privacy

- No content, credentials or connection strings are sent.
- Usage statistics are a separate, explicit opt-in that is **off** until an administrator turns it on, and the exact
  payload is shown first. See [Configuration](configuration.md#usage-statistics).
- On an unconnected installation, an editor can still send a single support report if
  `PublicReports` is enabled. See [Support and Feedback](support-and-feedback.md).

## Disconnecting

Disconnecting returns the installation to the unconnected behaviour described above: free capabilities keep working,
update and licence tiles return to **Not checked**.

## Related

- [Dashboard](dashboard.md)
- [Configuration](configuration.md)
- [Support and Feedback](support-and-feedback.md)
