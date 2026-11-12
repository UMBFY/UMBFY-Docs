# Support and Feedback

**What it does.** Lets you report a bug, request a feature or send feedback about a UMBFY package from inside the
Umbraco Backoffice, and shows what has already been raised from this installation.

**Where to find it.** **UMBFY → Support**.

**Required permissions.** The UMBFY section must be granted to your user group.

## Step-by-step

1. Open **UMBFY → Support**.
2. Choose what you are sending — bug report, feature request or general feedback.
3. Pick the package it concerns.
4. Describe the problem: what you did, what you expected, what happened instead.
5. Submit.

Your previous submissions are listed on the same page, so you can see whether something has already been raised
from this installation before sending a duplicate.

## Connected and unconnected installations

| | Connected account | No account |
| --- | --- | --- |
| Submit a report | Yes | Yes, if `PublicReports` is enabled |
| Report attached to your account | Yes | No |
| History kept across reports | Yes | Per report only |

On an unconnected installation, an editor sees an *Also send this report to UMBFY* option on an individual report.
It is off by default on every report, so it is always a deliberate choice. No domain, credentials or content is
sent. An administrator can remove the option entirely with
`UMBFY:Hub:PublicReports:Enabled` — see [Configuration](configuration.md#public-reports).

## What to include

- the package name and version, from [Packages](packages.md)
- your Umbraco version
- the installation id, from **UMBFY → Settings → About this installation**
- the steps that reproduce the problem

!!! danger "Never include secrets"
    Do not put passwords, connection strings, API keys or licence keys in a report or a public issue. If a log
    excerpt contains one, redact it first.

See [Reporting Issues](../shared/reporting-issues.md) and [Diagnostics](../shared/diagnostics.md).

## GitHub issues

For anything public — bugs, feature requests, discussion — the
[UMBFY Packages issue forms](https://github.com/UMBFY/UMBFY-Packages/issues) are the central tracker for every
package. The Backoffice form and the issue tracker are both valid routes; the issue tracker is public and
searchable, so prefer it for anything other users would benefit from seeing.

## Related

- [Reporting Issues](../shared/reporting-issues.md)
- [Diagnostics](../shared/diagnostics.md)
- [Configuration](configuration.md)
