# Impact

**What it does.** Shows an item's inbound and outbound relationships to a bounded depth, with a risk
classification.

**Why and when to use it.** Before changing something you suspect is load-bearing. [Where Used](where-used.md)
answers "who points at this?"; Impact answers "what does changing this touch?"

**Where to find it.** The **Impact** view on a content or media item's workspace.

**Required permissions.** Standard Umbraco permissions. Restricted items affect the risk rating without their
details being revealed.

**Edition.** **Professional.**

## Inbound versus outbound

| Direction | Question it answers |
| --- | --- |
| **Inbound** | What references this item — so what breaks if I remove or change it |
| **Outbound** | What this item references — so what this item depends on to render correctly |

An item with heavy inbound references is risky to change. An item with heavy outbound references is fragile to
others' changes. They are different problems and Impact separates them.

## Bounded depth

Dependency graphs can be large, and an unbounded walk of one is neither fast nor readable. Impact traverses to a
**bounded depth** and reports within it.

The practical consequence: Impact is a decision aid about the neighbourhood of a change, not an exhaustive
transitive closure of the whole site. Use [Content Health](content-health.md) for the site-wide picture.

## Risk classification

Impact classifies the likely risk of a change so an editor does not have to interpret raw counts. The inputs are the
shape of the dependency neighbourhood — how much depends on this item, how deeply, and the state of what is
involved.

Restricted content contributes to the rating without being named. An editor can therefore be correctly told a change
is risky because of content they are not permitted to see.

## Step-by-step

1. Open the content or media item.
2. Switch to the **Impact** view.
3. Read the risk classification first.
4. Expand inbound relationships to see what would break.
5. Expand outbound relationships to see what this item needs.
6. Decide, then act.

## Understanding the result

A low risk rating means the change is likely contained. A high rating means it reaches a lot of other content — not
that the change is wrong, only that it deserves care and probably a review.

Treat the rating as a prompt to look, not as permission or prohibition. The guards — [Safe Delete](safe-delete.md)
and [Publish Guard](publish-guard.md) — are what actually enforce policy.

## Examples

**A shared component.** An element used across thirty pages rates high inbound. Changing its structure is a project,
not a quick edit.

**A leaf page.** No inbound references, several outbound. Safe to change; worth knowing it depends on a shared image
and a navigation item.

**A hub page.** Heavy in both directions. The rating says "get a second pair of eyes", which is the right answer.

## Limitations

- Supported reference types only — see [Where Used](where-used.md#limitations).
- Bounded depth, by design. Not a full transitive graph of the site.
- Requires a **Ready** index for trustworthy results — see [Content Health](content-health.md).
- Risk classification is advisory. It does not block anything.

## Troubleshooting

| Symptom | Cause |
| --- | --- |
| Impact view unavailable | Free edition — Impact is Professional |
| Rating seems high for few visible relationships | Restricted content is contributing without being shown |
| Relationships look incomplete | The index is not **Ready**, or an unscanned property editor holds the reference |

See [Troubleshooting](troubleshooting.md).

## Related features

- [Where Used](where-used.md)
- [Content Health](content-health.md)
- [Safe Delete](safe-delete.md)
