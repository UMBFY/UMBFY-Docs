<section class="umbfy-product-hero">
  <span class="umbfy-product-hero__eyebrow">UMBFY PACKAGE · SCHEMA OPERATIONS</span>
  <h1>Environment Manager</h1>
  <p>Compare Umbraco schema between environments, plan a promotion, have it approved, execute it and verify the result afterwards — with deny-by-default mutation and a full audit trail.</p>
  <div class="umbfy-product-meta">
    <span>Umbraco 17</span>
    <span>Umbraco 18</span>
    <span>Release candidate</span>
    <span>Deny-by-default mutation</span>
  </div>
  <div class="umbfy-actions">
    <a class="umbfy-btn umbfy-btn--primary" href="installation/">Install Environment Manager</a>
    <a class="umbfy-btn umbfy-btn--ghost" href="quick-start/">Quick start</a>
  </div>
</section>

!!! warning "Release candidate — `1.0.0-rc.1`"
    Environment Manager is release-candidate packaging. It is not published to nuget.org and claims neither
    Marketplace approval nor live cloud certification. It **mutates schema on real environments**: exercise it
    between Local and Development before you point it at anything that matters.

## Start here

<div class="umbfy-doc-grid">
  <a class="umbfy-doc-card" href="installation/">
    <strong>Installation</strong>
    <span>Install on both ends of a promotion and let migrations run.</span>
  </a>
  <a class="umbfy-doc-card" href="configuration/">
    <strong>Configuration</strong>
    <span>Environment identity, inbound API key, timeouts and HTTPS rules.</span>
  </a>
  <a class="umbfy-doc-card" href="quick-start/">
    <strong>Quick Start</strong>
    <span>Register two environments, compare them and run your first promotion.</span>
  </a>
  <a class="umbfy-doc-card" href="troubleshooting/">
    <strong>Troubleshooting</strong>
    <span>Connection failures, refused paid actions and plans that will not execute.</span>
  </a>
</div>

## What it moves

Umbraco **schema**, specifically:

- Document Types
- Element Types
- Data Types
- Templates
- Dictionary items
- Languages

### What it deliberately does not do

Content and media sync, application or NuGet deployment, and database backup or restore are all **out of scope**.
Environment Manager moves schema only. Treating it as a content-deployment tool will disappoint you; treating it as
a schema-promotion tool with an audit trail will not.

## The safety model

Remote mutation is **deny-by-default**. There is exactly one path by which schema changes, and every step is
recorded:

```text
Compare → Plan → Approve → Execute → Verify → (Recover)
```

There is no shortcut from Compare to mutating Production. **Production** is an explicit environment type that
carries stronger acknowledgements than the others.

## Core features

### Environments and connectivity

Register Local, Development, Staging and Production peers, then prove connectivity before anything can be promoted.

[Read the Environments guide &rarr;](environments.md)

### Compare and drift

Capture schema snapshots, compare two environments and detect drift, with dependency mapping so you can see what a
change pulls in with it.

[Read the Compare and Drift guide &rarr;](compare-and-drift.md)

### Promotion

Build an immutable promotion plan from selected differences, gate it behind approval, and execute it against the
destination. The approved plan's fingerprint is bound, so an altered plan cannot be executed.

[Read the Promotion guide &rarr;](promotion.md)

### Verification

After execution, independently re-read the destination and confirm it matches what was planned — rather than
trusting the executor's own report.

[Read the Verification guide &rarr;](verification.md)

### Recovery

Assess and execute recovery for supported managed schema when a promotion did not land as intended.

[Read the Recovery guide &rarr;](recovery.md)

### Bootstrap

Bring a near-empty destination up from a source snapshot in one controlled operation, instead of promoting
difference by difference.

[Read the Bootstrap guide &rarr;](bootstrap.md)

### Deployments

Full history with paging, filters and live progress for anything still running.

[Read the Deployments guide &rarr;](deployments.md)

## Editions

| Edition | Includes |
| --- | --- |
| **Free** | Dashboard, connection diagnostics, snapshots, compare, basic drift — **no Hub and no licence required** |
| **Professional** | Free, plus promotion plan and execute, bootstrap, verification, recovery, multi-environment, advanced cluster and advanced approvals |
| **Agency** | Professional, plus advanced governance |
| **Enterprise** | Agency, plus enterprise integration hooks |

Licences count **logical environments**, not application nodes — a load-balanced site with four servers is one
environment, not four.

[Read the Editions and Licensing guide &rarr;](editions-and-licensing.md)

## Install

```bash
dotnet add package UMBFY.Umbraco.EnvironmentManager --version 1.0.0-rc.1
```

Install it on **both** ends of any promotion. No Node.js is required. See
[Installation](installation.md).

## Two different credentials

A recurring source of confusion worth stating up front:

| Credential | What it is for |
| --- | --- |
| **Signed licence** (or a Hub-reported licence) | Which *product features* you may use |
| **Environment API key** | Authenticating Environment Manager calls *between your own Umbraco sites* |

Activating a licence does not grant remote access. Rotating an API key does not change your entitlements.

[Read the Security guide &rarr;](security.md)

## Hosting and clustering

Single-node hosting is supported. Multi-node hosting with a shared database and fencing is architecturally
supported and was exercised against a disposable Docker cluster; live cloud certification is not claimed. Shared
hosting is often partial or blocked for multi-node.

## Documentation map

<div class="umbfy-doc-grid">
  <a class="umbfy-doc-card" href="environments/"><strong>Environments</strong><span>Register peers and prove connectivity.</span></a>
  <a class="umbfy-doc-card" href="compare-and-drift/"><strong>Compare and Drift</strong><span>Snapshots, differences and drift detection.</span></a>
  <a class="umbfy-doc-card" href="promotion/"><strong>Promotion</strong><span>Plan, approve and execute a schema change.</span></a>
  <a class="umbfy-doc-card" href="verification/"><strong>Verification</strong><span>Independently confirm the destination.</span></a>
  <a class="umbfy-doc-card" href="recovery/"><strong>Recovery</strong><span>Assess and recover supported managed schema.</span></a>
  <a class="umbfy-doc-card" href="bootstrap/"><strong>Bootstrap</strong><span>Bring a near-empty destination up from a snapshot.</span></a>
  <a class="umbfy-doc-card" href="deployments/"><strong>Deployments</strong><span>History, filters and live progress.</span></a>
  <a class="umbfy-doc-card" href="editions-and-licensing/"><strong>Editions and Licensing</strong><span>What each edition includes and how sites are counted.</span></a>
  <a class="umbfy-doc-card" href="security/"><strong>Security</strong><span>API keys, HTTPS, permissions and the audit trail.</span></a>
</div>

## Support

Use the [UMBFY Packages issue forms](https://github.com/UMBFY/UMBFY-Packages/issues). Include the package version,
your Umbraco version and the environment types involved. Never include API keys, licence keys or connection strings
in a public issue.
