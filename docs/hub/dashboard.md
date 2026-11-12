# Hub Dashboard

**What it does.** Answers "is my UMBFY installation healthy?" in one screen.

**When to use it.** First stop after installing or upgrading any UMBFY package, and whenever a package reports a
problem.

**Where to find it.** **UMBFY → Dashboard**.

**Required permissions.** The UMBFY section must be granted to your user group. Administrative actions on this page
require a Backoffice administrator.

## The three tiles

| Tile | What it answers | States you will see |
| --- | --- | --- |
| **Health** | Is any installed package reporting an error or a warning? | Healthy, warnings, errors |
| **Updates** | Is a newer version available for anything installed? | Up to date, updates available, Not checked |
| **Account** | Is this installation connected to a UMBFY account? | Connected, not connected |

### Reading the times

Hub writes relative times — *Checked 5 minutes ago* — because what matters is whether the information is fresh,
not the exact clock value.

**Not checked** is not an error. It means no UMBFY account is connected, so Hub has had no opportunity to check
anything. Free capabilities are unaffected. See [UMBFY Account](account.md).

## Needs attention

A single list of everything actionable, so you do not have to walk the whole section looking for problems. It
collects:

- package **errors**
- package **warnings**
- **available updates**
- **licence problems** — expired, missing or unusable licences
- **account not connected**

Each entry links to the place where the problem is fixed. An empty list is the goal state.

## Installed packages

Below the attention list, every installed UMBFY package appears in one table with its status and version. For the
richer per-package view — update availability, licence state and documentation links — open
[Packages](packages.md).

## Understanding the result

A healthy installation shows: Health green, Updates either up to date or honestly reporting available updates, and
an empty **Needs attention** list. If the account is deliberately left unconnected, expect **Not checked** on the
updates tile permanently — that is a correct report, not a failure.

## Limitations

- Update and licence information requires a connected UMBFY account. Without one, Hub does not guess.
- Hub reports what each installed package tells it. A package that failed to load does not appear at all — see
  [Troubleshooting](troubleshooting.md).

## Related

- [Packages](packages.md)
- [UMBFY Account](account.md)
- [Troubleshooting](troubleshooting.md)
