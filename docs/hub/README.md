<section class="umbfy-product-hero">
  <span class="umbfy-product-hero__eyebrow">UMBFY PACKAGE · ECOSYSTEM HOME</span>
  <h1>Hub</h1>
  <p>The shared UMBFY home in the Umbraco Backoffice. Every UMBFY package registers itself with Hub, so one section tells you what is installed, what needs attention, what has an update available, and the state of your UMBFY account.</p>
  <div class="umbfy-product-meta">
    <span>Umbraco 17</span>
    <span>Umbraco 18</span>
    <span>Backoffice integrated</span>
    <span>Installed with every package</span>
  </div>
  <div class="umbfy-actions">
    <a class="umbfy-btn umbfy-btn--primary" href="installation/">Install Hub</a>
    <a class="umbfy-btn umbfy-btn--ghost" href="quick-start/">5-minute quick start</a>
  </div>
</section>

## Start here

<div class="umbfy-doc-grid">
  <a class="umbfy-doc-card" href="installation/">
    <strong>Installation</strong>
    <span>Install the package and grant the UMBFY section to the right user groups.</span>
  </a>
  <a class="umbfy-doc-card" href="quick-start/">
    <strong>Quick Start</strong>
    <span>Open the UMBFY section, read the dashboard and resolve what needs attention.</span>
  </a>
  <a class="umbfy-doc-card" href="configuration/">
    <strong>Configuration</strong>
    <span>Branding, public reports and usage statistics — all optional, all off-by-default where it matters.</span>
  </a>
  <a class="umbfy-doc-card" href="troubleshooting/">
    <strong>Troubleshooting</strong>
    <span>Missing section, packages not listed, everything reading "Not checked".</span>
  </a>
</div>

## You rarely install Hub on purpose

Every UMBFY package depends on Hub, so installing any one of them installs Hub. You install it directly only when
you want the UMBFY section before any feature package is in place.

Because Hub is a dependency of the others, it is also the package to **uninstall last**.

## What Hub gives you

### Dashboard

Health, updates and account tiles, a **Needs attention** list, and every installed UMBFY package in one table.
The attention list surfaces errors, warnings, available updates, licence problems and a not-yet-connected account.

[Read the Dashboard guide &rarr;](dashboard.md)

### Packages

One card per installed package: status, installed version, whether an update is available, licence state, and a link
to that package's documentation. Packages with problems sort to the top.

[Read the Packages guide &rarr;](packages.md)

### Settings

Every package that exposes settings, each with an **Open settings** action, plus **About this installation** — Hub
version, package count, connected account and installation id.

[Read the Configuration guide &rarr;](configuration.md)

### Support

Report a bug, request a feature or send feedback from inside the Backoffice, with your previous submissions listed
so you can see what has already been raised.

[Read the Support and Feedback guide &rarr;](support-and-feedback.md)

## The UMBFY account

Hub works without an account. Until you connect one, nothing is sent anywhere and every free capability keeps
working — Hub simply cannot tell you about updates or licences, so time-based tiles read **Not checked**.

Connecting an account enables licence sync, update checks and support history.

[Read the UMBFY Account guide &rarr;](account.md)

## Install

```bash
dotnet add package UMBFY.Umbraco.Hub
```

No Node.js and no client build step — the package ships compiled Backoffice assets under
`/App_Plugins/UMBFY.Hub/`.

See [Installation](installation.md) for the full procedure, including the user-group step that is easy to miss.

## Security and privacy

- Hub never sends anything to UMBFY until an administrator connects an account or explicitly opts in per report.
- Usage statistics are **off** until an administrator opts in, and the exact payload is shown before you do.
- Backoffice branding is **off** by default, so installing a package never rebrands a site on its own.
- Access to the UMBFY section is controlled by standard Umbraco user-group section permissions.

## Documentation map

<div class="umbfy-doc-grid">
  <a class="umbfy-doc-card" href="dashboard/"><strong>Dashboard</strong><span>Health, updates, account and the Needs attention list.</span></a>
  <a class="umbfy-doc-card" href="packages/"><strong>Packages</strong><span>Installed packages, versions, updates and licence state.</span></a>
  <a class="umbfy-doc-card" href="account/"><strong>UMBFY Account</strong><span>Connect, what it enables, what is sent, how to disconnect.</span></a>
  <a class="umbfy-doc-card" href="support-and-feedback/"><strong>Support and Feedback</strong><span>Raise bugs and requests from the Backoffice.</span></a>
  <a class="umbfy-doc-card" href="configuration/"><strong>Configuration</strong><span>Branding, public reports, usage statistics.</span></a>
  <a class="umbfy-doc-card" href="faq/"><strong>FAQ</strong><span>Short answers to the questions that come up first.</span></a>
</div>

## Support

Use the [UMBFY Packages issue forms](https://github.com/UMBFY/UMBFY-Packages/issues) for bugs, feature requests and
package support. Include the Hub version and your Umbraco version. Never include passwords, connection strings, API
keys or licence keys in a public issue.
