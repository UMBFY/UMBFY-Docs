# Content Guard FAQ

**Do I have to re-save my existing content for it to be indexed?**
No. Content Guard bootstraps the dependency index automatically on first start. On a large site give it a few
minutes; [Content Health](content-health.md) shows the progress.

**What does Content Guard do while the index is still building?**
It fails closed. The guards will not claim an item is safe to delete or a page safe to publish from a half-built
index. Being briefly cautious is the intended behaviour.

**What can it actually detect?**
Content Picker, media references, Multi URL Picker internal links, Rich Text internal links, and those same editors
nested inside Block Grid / Block List. Culture-specific values are handled. External URLs are not treated as
internal dependencies.

**My custom property editor's references don't show up.**
They will not until support is registered with
`builder.AddContentGuardReferenceProvider<MyEditorReferenceProvider>()`. Until then, items referenced only by that
editor look unreferenced — which matters before you set a delete policy to `Block`.

**What do I get for free?**
[Where Used](where-used.md) in full, and [Safe Delete](safe-delete.md) in `Warn` mode. You always see what
references an item before you change it. See [Editions](editions.md).

**If my licence lapses, does my site stop working?**
No. Licensing **downgrades, it never blocks**. A configured `Block` policy behaves as `Warn`, Publish Guard stands
down, and deleting and publishing keep working.

**Then why is my `Block` policy behaving as `Warn`?**
Almost certainly the edition. A configured policy is a ceiling, not a guarantee.

**Is the index rebuild a paid feature?**
No, on any edition — Where Used is free and cannot work without the index. It does require an administrator,
because it re-reads the whole tree.

**Does it modify my content?**
No. Content Guard reads content and reports on it. Removing the package leaves content untouched.

**Can editors see references to content they're not allowed to see?**
No. Restricted references are **counted but not revealed**, so an editor learns that something they cannot see
depends on an item without the names leaking. This is why a count can exceed the visible rows.

**Should I use `Warn`, `RequireConfirmation` or `Block`?**
`RequireConfirmation` is the default and suits most teams. Run `Warn` for a fortnight on an existing site to see
what it reports, then tighten. Only move to `Block` once you have registered scanners for your custom editors.

**Can I guard deletes strictly but publishes loosely?**
Yes. The three feature switches are independent. A strict delete policy with a permissive publish policy is a common
arrangement, since a bad publish is easier to reverse.

**Why did my site refuse to start after I changed the settings?**
By design. A TTL outside 30–3600 seconds, a `VisibleTake` outside 1–100, or an unknown policy name is a
configuration error rather than a silent fallback — a typo that quietly reverted to `Warn` would leave the site less
protected than you believed.

**Does it work on multilingual sites?**
Yes, and culture-aware validation is an **Agency** capability. It handles missing cultures, unpublished cultures and
unavailable fallback targets. See [Multilingual Validation](multilingual-validation.md).

**What's the difference between Where Used and Impact?**
Where Used answers "who points at this?" (inbound). Impact adds outbound relationships, bounded depth and a risk
rating — "what does changing this touch?"

**Which Umbraco versions are supported?**
17.x and 18.x (`[17.0.0,19.0.0)`). See
[Supported Umbraco versions](../getting-started/supported-umbraco-versions.md).

**Where do I report a bug?**
The [UMBFY Packages issue tracker](https://github.com/UMBFY/UMBFY-Packages/issues). Never include connection
strings, credentials or licence keys.
