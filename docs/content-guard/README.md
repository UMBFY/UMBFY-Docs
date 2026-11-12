<section class="umbfy-product-hero">
  <span class="umbfy-product-hero__eyebrow">UMBFY PACKAGE · CONTENT SAFETY</span>
  <h1>Content Guard</h1>
  <p>Understand content relationships before changes cause broken references. Content Guard gives editors, administrators and agencies dependency intelligence directly inside the Umbraco Backoffice.</p>
  <div class="umbfy-product-meta">
    <span>Umbraco 17</span>
    <span>Umbraco 18</span>
    <span>Backoffice integrated</span>
    <span>Dependency intelligence</span>
  </div>
  <div class="umbfy-actions">
    <a class="umbfy-btn umbfy-btn--primary" href="installation/">Install Content Guard</a>
    <a class="umbfy-btn umbfy-btn--ghost" href="quick-start/">10-minute quick start</a>
  </div>
</section>

## Start here

<div class="umbfy-doc-grid">
  <a class="umbfy-doc-card" href="installation/">
    <strong>Installation</strong>
    <span>Install the package, start Umbraco and verify the dependency index is ready.</span>
  </a>
  <a class="umbfy-doc-card" href="quick-start/">
    <strong>Quick Start</strong>
    <span>Create a real reference, inspect Where Used and verify Content Guard end to end.</span>
  </a>
  <a class="umbfy-doc-card" href="configuration/">
    <strong>Configuration</strong>
    <span>Configure guard policies, result limits, multilingual validation and operational behaviour.</span>
  </a>
  <a class="umbfy-doc-card" href="troubleshooting/">
    <strong>Troubleshooting</strong>
    <span>Diagnose index health, scanner problems, permissions and package-specific runtime issues.</span>
  </a>
</div>

## What Content Guard protects

Content Guard helps teams understand where content is referenced, prevent unsafe deletion and publishing, monitor content health, validate multilingual relationships, and assess downstream impact before making changes.

It is designed for:

- Editors who need confidence before changing, unpublishing, or deleting content
- Administrators responsible for content integrity across large sites
- Agencies managing complex Umbraco implementations with many references
- Multilingual teams that need culture-aware dependency validation
- Developers who want durable dependency information without repeatedly scanning the full content tree

## Core features

### Where Used

Shows which content or media items reference the current item, including source name, property context, path, culture/segment, state, and authorization-aware navigation.

[Read the Where Used guide →](where-used.md)

### Safe Delete

Protects referenced content and media from accidental deletion. Supported policies are Warn, Require Confirmation, and Block. Safety decisions fail closed when the dependency index is incomplete or unhealthy.

[Read the Safe Delete guide →](safe-delete.md)

### Publish Guard

Detects unhealthy dependencies before publishing, including missing, trashed, unpublished, and culture-specific dependency problems.

[Read the Publish Guard guide →](publish-guard.md)

### Content Health

Provides a centralized view of dependency integrity with status, metrics, paging, filters, and explicit index-health states.

[Read the Content Health guide →](content-health.md)

### Multilingual Validation

Validates references across cultures and language fallback behavior, including missing or unpublished cultures and unavailable fallback targets.

[Read the Multilingual Validation guide →](multilingual-validation.md)

### Dependency Impact

Shows inbound and outbound relationships, bounded dependency depth, and risk classification so editors can understand the likely effect of a change before making it.

[Read the Impact guide →](impact.md)

## Editions

| Edition | What you get |
| --- | --- |
| **Free** | Where Used, and Safe Delete in `Warn` mode |
| **Professional** | + Safe Delete `RequireConfirmation` / `Block`, Publish Guard, Content Health, Impact |
| **Agency** | + multilingual validation, custom reference providers, reporting |

Licensing **downgrades, it never blocks**. On a Free installation a configured `Block` policy behaves as `Warn` and
Publish Guard stands down, so deleting and publishing keep working — a site is never held hostage to a licence.
Index rebuild is never licence-gated, because Where Used is free and cannot work without the index.

[Read the Editions guide →](editions.md)

## Supported reference types

- Content Picker
- Media references
- Multi URL Picker internal links
- Rich Text Editor internal links
- Supported nested references inside Block Grid / Block List structures
- Culture-specific reference values

External URLs are not treated as internal content dependencies. Third-party custom property editors require explicit scanner support.

## Existing-site bootstrap

On first installation, Content Guard creates its durable dependency-index storage and bootstraps existing content automatically. Existing content does not need to be manually re-saved.

```bash
dotnet add package UMBFY.Umbraco.ContentGuard
```

See [Installation](installation.md) for the complete setup and verification procedure.

## Security and permissions

Content Guard respects Umbraco Backoffice permissions. Restricted dependencies may still affect risk and guard decisions without exposing restricted names or details to unauthorized users.

## Operations

The durable dependency index powers Where Used, Safe Delete, Publish Guard, Content Health, and Impact. Important operational states include **Initializing**, **Rebuilding**, **Ready**, and **Unhealthy**. When completeness matters, an incomplete index must never be reported as safe or healthy.

See [Rebuild Index](rebuild-index.md) and [Troubleshooting](troubleshooting.md).

## Documentation map

<div class="umbfy-doc-grid">
  <a class="umbfy-doc-card" href="where-used/"><strong>Where Used</strong><span>Find inbound references and navigate back to their source.</span></a>
  <a class="umbfy-doc-card" href="safe-delete/"><strong>Safe Delete</strong><span>Protect referenced content and media from unsafe deletion.</span></a>
  <a class="umbfy-doc-card" href="publish-guard/"><strong>Publish Guard</strong><span>Detect unhealthy dependencies before content is published.</span></a>
  <a class="umbfy-doc-card" href="content-health/"><strong>Content Health</strong><span>Review dependency health and index status centrally.</span></a>
  <a class="umbfy-doc-card" href="multilingual-validation/"><strong>Multilingual Validation</strong><span>Validate culture-aware references and language fallback behaviour.</span></a>
  <a class="umbfy-doc-card" href="impact/"><strong>Impact Analysis</strong><span>Understand inbound and outbound dependency impact before a change.</span></a>
  <a class="umbfy-doc-card" href="editions/"><strong>Editions</strong><span>What Free, Professional and Agency include, and why licensing downgrades.</span></a>
  <a class="umbfy-doc-card" href="tutorials/"><strong>Tutorials</strong><span>Task-oriented walkthroughs for the workflows editors actually run.</span></a>
</div>

## Screenshots and guided workflows

The UMBFY documentation standard treats real Umbraco Backoffice screenshots as part of the product documentation. Feature pages should show the actual UI, then explain the workflow step by step. Screenshot assets are maintained using the shared [Screenshot Guide](../shared/screenshot-guide.md).

## Support

Use the UMBFY Packages issue forms for bugs, feature requests, and package support. Include the package version and Umbraco version when reporting a problem. Never include passwords, connection strings, API keys, license keys, or other secrets in public issues.
