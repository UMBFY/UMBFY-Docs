# Promotion

**What it does.** Moves selected schema from a source environment to a destination through an immutable plan, an
approval gate and a recorded execution.

**When to use it.** Whenever schema must move between environments in a way you can audit afterwards.

**Where to find it.** **Environment Manager → Compare**, then the plan and deployment views.

**Required permissions.** The Environment Manager section. Approving a plan is a deliberate, recorded act.

**Edition.** Professional and above.

## Deny-by-default

There is exactly one path by which Environment Manager changes schema on a destination:

```text
Compare → Plan → Approve → Execute → Verify → (Recover)
```

There is no shortcut from Compare to mutating Production, and every step is recorded. If you are looking for a
one-click "push to live", it does not exist on purpose.

## 1. Compare

Snapshot both environments and read the differences, including what each change depends on. See
[Compare and Drift](compare-and-drift.md).

## 2. Plan

Select the differences to promote and build a plan.

The plan is **immutable** and its fingerprint is bound to its contents. That is what makes approval meaningful: an
approval applies to the exact plan that was approved, not to a plan that was edited afterwards.

A plan records what will be created and what will be changed on the destination, so it can be read and challenged
before anyone approves it.

## 3. Approve

Approve the plan.

On a real team the approver need not be the planner, and the approval is recorded against the plan. Advanced
approval workflows are a Professional capability; the gate itself is not optional.

## 4. Execute

Execute the approved plan against the destination.

- Progress is live.
- The run appears in [Deployments](deployments.md) while it is running and stays there afterwards.
- On a multi-node destination, execution is fenced so two nodes do not apply the same plan.

### Production

When the destination's `LocalEnvironmentType` is `Production`, execution requires stronger acknowledgement than
elsewhere. This is deliberate friction. Do not neutralise it by mislabelling Production as Staging — the label is
what the extra control hangs off.

## 5. Verify

Independently re-read the destination and confirm it matches the plan. Treat a promotion as incomplete until it has
verified. See [Verification](verification.md).

## Why a plan stops being executable

A plan is built from a specific snapshot pair. If the schema on either end moves after the plan was built, the plan
no longer describes reality and its fingerprint no longer matches what approval was given for.

When that happens, **re-compare and re-plan**. Do not look for a way to force an old plan through; the fingerprint
check is the control that makes the audit trail trustworthy.

## Understanding the result

A complete promotion gives you: a recorded plan, a recorded approval, a recorded execution with its outcome, and an
independent verification that the destination matches. That set is the audit trail. If any one of them is missing,
you have a schema change you cannot account for.

## Limitations

- Schema only. Content, media, binaries and database restore are out of scope.
- Both ends need the package at the same version.
- Promotion requires proven connectivity — see [Environments](environments.md).

## Troubleshooting

| Symptom | Cause |
| --- | --- |
| A paid action is refused | Free edition, or no usable licence. See [Editions and Licensing](editions-and-licensing.md). |
| The plan will not execute | It needs approval, or the schema moved underneath it and the fingerprint no longer matches. Re-plan. |
| Execution fails partway | Review the deployment record, then [Recovery](recovery.md). |

See [Troubleshooting](troubleshooting.md).

## Related

- [Verification](verification.md)
- [Recovery](recovery.md)
- [Deployments](deployments.md)
