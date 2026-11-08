# Manifest-defined UI and actual consumers

Read this when explaining or adapting a model's discovery, forms, actions,
repair/solution panels or result views. Use the selected producer's canonical
**authoring/UI manifest schema**, distinct from runtime model and solve request
contracts. Do not invent a second UI configuration format or assume a runtime
manifest carries all presentation fields.

## Offer an optional management UX

Once a new/adapted problem brief is understood, ask whether the user wants a UX
to configure the model and manage/monitor solves. Offer this even when no UI
metadata exists and the user has not mentioned a UI. For example: “Would you
like a UI to edit the model's inputs and constraints, submit solves, track their
status, inspect/compare results and request repairs?” This is an optional scope
choice, not a prerequisite for solving.

Reuse a prior choice. Respect a decline; do not repeat the offer during every
refinement. If unanswered, continue supported manifest/non-UI work without
creating a UI. If accepted, ask only unresolved questions about users, editable
facts/constraints/objectives, submission/cancellation, status, result views,
comparison/history and repair needs. These are needs to verify against actual
contracts, not promises that every operation is available.

Use canonical authoring/UI declarations and existing shared components and
consumer extension points. For a new application, use Nuxt/PrimeVue, reuse
`@platform/*` and `@helixor/common-ux`, and generate cross-tier seams with
`helixor-sdk-gen`. Verify applicable release contracts before implementation;
do not create a second UI schema, parser, renderer or hand-written service client.
Declaring a panel alone does not build a working management UI.

Monitoring uses supported events/push/streams or user-initiated refresh. A UX
request does not authorize polling. Keep polling disabled unless explicit human
approval identifies target, purpose, interval, request/storage cost, backoff and
jitter, idle/visibility behavior, termination and why event/push/watch/stream/
queue/manual refresh cannot meet the need. Do not invent event support; use
manual refresh or report the exact contract gap when needed.

## Trace the whole chain

Keep these states separate: declared → schema-valid → delivered → consumed →
rendered → authorized execution. For each material element record its stable
manifest ID/path, manifest/service/UI build versions, delivery source, consumer
component/state, input/request or result binding, and actual observation or gap.
This is an explanation/evidence table, not a new executable schema.

| Concern | What to inspect and preserve |
| --- | --- |
| Discovery and surfaces | Effective visibility/hidden state; enabled/disabled/absent surface definitions; primary/label/title hints; local overrides and documented legacy behavior. Follow service summaries/details into the actual selector; listed availability is not consumer filtering |
| Input controls | Actual field source, which may include input/category definitions and applicable UI/constraint/objective/preset declarations. Do not assume `ui.params` generates every form |
| Control semantics | Stable IDs, labels/help, types, defaults, units, requiredness, bounds/steps, choices, grouping and supported widget hints. Preserve zero, false, null and missing distinctions through edits and submission |
| Actions and requests | Trace the control through state to the submitted producer field/operation, preparation validity and authorization. A visible repair control or enabled surface is not an enforced pin or granted operation |
| Repair/solution panels | Inspect declared panels, nested fields and view hints, then identify actual panel/action/result consumers and installed renderers. A declaration alone does not create one |
| Adaptation and reuse | Preserve compatible UI metadata and deliberate UI changes with model deltas and versioned bindings; check renamed inputs/rules/result IDs, stale defaults and reload behavior |

A UI-only presentation gap does not establish that the solver model is unavailable
through another supported interface. Conversely, a visible field, default or
required marker does not establish valid instance facts or producer enforcement.
Keep validation/admission and authority at the producer boundary.

## Author and check changes

During [pattern adaptation or custom definition](modeling.md), inventory the
original canonical UI declarations alongside the model/data rules. Preserve
compatible metadata and show deliberate presentation/binding changes. Map new
or renamed IDs through form state, request fields and result consumers; do not
silently drop metadata when emitting a candidate artifact.

Run canonical validation and, where the target supports it, load/edit/save/reload
checks on the actual artifact. Inspect the resulting artifact/version as well
as visible controls. No connected UI or MCP is needed to explain/author a
candidate, but observed consumption remains a separately qualified result.

For malformed/unknown widgets, absent optional hints, unsupported panels or
stale/mismatched versions, describe the actual failure and its scope. An
existing generic view/control is adequate only if it preserves all required
meaning and bindings. Otherwise identify the exact owning schema/consumer
extension gap. Do not create app-local parsing, a replacement renderer, guessed
result fields or an ad hoc configuration to make an example appear supported.

## Synthetic UI exercises

These are test situations, not canonical manifest payloads or browser results:

- A service summary lists a model, but its surface is disabled or the selected
  UI hides it locally. Trace the effective selector state; visibility does not
  confer authority. For an absent surface, inspect the documented version's
  behavior rather than choosing a universal default.
- A numeric input has a declared minimum and a zero value; a boolean is false;
  another required fact is null. Capture the rendered control and submitted
  values. A display default must not supply a missing business fact; an invalid
  value must retain the producer's diagnostic rather than silently clamp.
- A repair panel declares a frozen baseline field, but no installed consumer
  sends it. The panel declaration cannot prove preservation. Use a supported
  adequate input path or state the exact gap before dependent execution.
- An adapted model renames an input/result ID. Validate dangling bindings,
  inspect save/reload behavior and ensure old cached defaults are not applied
  to the new version. Record intentional UI changes with the model delta.
- A result has no specialized renderer. Show stable IDs, units, verdict,
  shortfalls and partial/failed states using an adequate existing generic view;
  do not invent a timeline, coordinate or certificate field.

## Evidence for an actual UI acceptance run

Select compatible UI build, manifest/model and service versions. For applicable
discovery/form/repair/solution fixtures, retain:

1. The declaration and service summary/detail delivery path, including version
   and effective visibility/surface settings.
2. Observed rendered controls/state and edited values, with screens or supported
   UI-state evidence. Source code inspection alone is not a browser pass.
3. Redacted submitted requests and their canonical validation/admission/authority
   verdicts. Exercise missing required, invalid/boundary and permission-denied
   paths; no UI flag may bypass producer checks.
4. Bound result/repair states and IDs, units, missing/failed/partial rendering,
   and supported roundtrip/reload behavior after a model edit.

Label unsupported or unavailable consumer paths precisely and keep checks
`not_run`/`blocked` until exercised. Do not infer actual behavior from a schema,
summary, renderer name or prepared fixture. Continue supported non-UI modeling
and service paths independently. See [inputs](inputs-and-execution.md),
[results/repair](results-and-repair.md) and [lifecycle](lifecycle-and-feedback.md).
