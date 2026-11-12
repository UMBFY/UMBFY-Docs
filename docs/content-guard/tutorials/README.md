# Content Guard Tutorials

Task-oriented walkthroughs for the workflows editors and administrators actually run. Each one names the scenario,
what edition it needs, and how to read the result — including when the result is misleading.

<div class="umbfy-doc-grid">
  <a class="umbfy-doc-card" href="find-existing-references/">
    <strong>Find existing references</strong>
    <span>Answer "what uses this?" for one item, with the property context that makes it actionable. Free.</span>
  </a>
  <a class="umbfy-doc-card" href="protect-content-before-delete/">
    <strong>Protect content before deletion</strong>
    <span>Remove an item without breaking the pages that use it, and deal with the references first.</span>
  </a>
  <a class="umbfy-doc-card" href="validate-multilingual-content/">
    <strong>Validate multilingual content</strong>
    <span>Publish a culture variant without leaving gaps that only show in that language. Agency.</span>
  </a>
</div>

## Start with the index

Every tutorial begins the same way, because every Content Guard answer depends on it: check the dependency-index
state on [Content Health](../content-health.md) and wait for **Ready**.

While the index is **Initializing**, **Rebuilding**, **Unhealthy** or **Failed**, the guards fail closed and results
are incomplete. Conclusions drawn in that window are about the index, not about your content.

## The one caveat that applies throughout

A custom or third-party property editor is not scanned until support is registered. An item referenced **only** by
such an editor looks unreferenced — which is the one way these workflows can tell you a change is safe when it is
not.

See [Where Used limitations](../where-used.md#limitations) and
[Configuration](../configuration.md#custom-property-editors).

## Related

- [Quick Start](../quick-start.md) — if you have not verified the installation yet
- [Where Used](../where-used.md) · [Safe Delete](../safe-delete.md) · [Impact](../impact.md)
- [FAQ](../faq.md)
