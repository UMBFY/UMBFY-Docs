# Hub Quick Start

About five minutes. This walks the UMBFY section end to end so you know what Hub is telling you.

**Before you start:** Hub installed and the **UMBFY** section granted to your user group — see
[Installation](installation.md).

## 1. Open the UMBFY section

Reload the Backoffice and choose **UMBFY** from the section menu. You land on the **Dashboard**.

If the section is not there, your user group does not have it. Go back to
[Installation step 3](installation.md#3-grant-the-umbfy-section-to-a-user-group).

## 2. Read the tiles

The dashboard opens with three summary tiles:

| Tile | What it answers |
| --- | --- |
| **Health** | Is anything reporting an error or warning right now? |
| **Updates** | Does any installed package have a newer version available? |
| **Account** | Is this installation connected to a UMBFY account? |

Times are written the way people read them — *Checked 5 minutes ago* rather than a raw timestamp. **Not checked**
means no account is connected, so Hub has not been able to check anything yet. That is expected on a fresh install
and nothing is broken.

## 3. Work the "Needs attention" list

Below the tiles, **Needs attention** collects everything actionable in one place: package errors, warnings,
available updates, licence problems and a not-yet-connected account. An empty list is the goal state.

Each entry links to the place where you fix it.

## 4. Review installed packages

Open **Packages**. You get one card per installed UMBFY package showing:

- current status
- installed version, and whether an update is available
- licence state
- a link to that package's documentation

Packages with problems sort to the top, so the first card is the one worth your attention.

If a package you installed is missing from this list, see [Troubleshooting](troubleshooting.md).

## 5. Find a package's own settings

Open **Settings**. Every package that exposes configuration is listed with an **Open settings** action that takes
you straight to it, so you do not have to remember which section a given package put its settings in.

The same page carries **About this installation** — Hub version, package count, connected account and installation
id. Quote the installation id when you raise a support issue.

## 6. Optional: connect your UMBFY account

**Dashboard → Connect UMBFY Account.**

Everything free keeps working whether you connect or not. Connecting is what enables licence sync, update checks and
support history. Until you do, nothing is sent anywhere.

See [UMBFY Account](account.md) for exactly what connecting does.

## 7. Optional: raise something

Open **Support** to report a bug, request a feature or send general feedback without leaving the Backoffice. Your
previous submissions are listed, so you can see what has already been raised from this installation.

See [Support and Feedback](support-and-feedback.md).

## Next

- [Dashboard](dashboard.md) — each tile and attention state in detail
- [Configuration](configuration.md) — the three optional settings and when to change them
- [FAQ](faq.md)
