# Adapt a pattern or define a custom model

Use existing canonical manifests, typed contracts, validators and shared
extension points. A language model may propose the interpretation and artifact;
validation/admission and independent evaluation determine executable truth.
Do not write a bespoke allocator, scoring loop, parser or parallel model schema.

For LLM-generated formulations, read [formulation guidance](formulation.md)
for symbolic lowering, variable binding, source coverage and missing-input
distinctions. It applies only within the selected contract's supported scope.

## Conversation before implementation

Use this sequence for new/adapted models in both hosted and embedded journeys.
Runtime placement does not change the business modeling obligations.

1. Reuse the brief, existing manifest, data and prior answers. Identify decisions,
   mandatory rules, preferences, objectives and unknowns. Inspect the closest
   canonical manifest's input requirements and clarification metadata.
2. Ask a small focused batch of unresolved questions that change the model,
   starting with decisions and hard constraints, then objective tradeoffs and
   required facts. Explain why an ambiguity matters. Wait for model-changing
   answers before implementing or executing dependent work; continue independent
   discovery while waiting. Do not silently choose business facts or defaults.
3. Show the evolving model in plain language: what is chosen, what is fixed,
   what must hold, what may be traded off, how success is ranked, and which data
   or assumptions remain unresolved. [Attribute each fact and constraint](#attribute-facts-and-constraints)
   before labeling it supplied or required. Correct ambiguity with the user. Do not add
   a generic approval step when the requirements and authorization are clear.
4. Use Path A or B below to author the candidate in the producer's established
   manifest/model format. Keep each material rule/objective linked to its input,
   declaration, hard/soft priority and validation/evaluation check. Validate
   schema, admission and actual rule behavior as applicable. A rule's presence
   in JSON/YAML does not establish enforcement. Missing contracts produce a
   useful brief and an exact gap, not invented configuration.
5. Build integration code only after this model and its required semantics are
   established and validated. Do not replace configuration with app-local rule
   logic. Reuse a supplied validated model and prior evidence; integration-only
   maintenance needs relevant gap checks, not another interview. A request to
   write code does not answer missing business constraints.
6. Once the brief is understood, proactively [offer the optional management UX](manifest-ui.md#offer-an-optional-management-ux).
   Keep that choice separate from model correctness and execution placement.

If a required rule cannot be expressed or evaluated, stop the dependent solve
and any claim that the full problem is feasible. Investigate canonical
composition or the owning extension; retain the rule in the model brief.
Only a separately requested limited demonstration may omit it: identify the
omissions before execution and scope every result to the demonstrated subset.
Disclosure after a run is not evidence that the original requirements held.
An unavailable hosted endpoint does not authorize switching to embedded mode.

## Attribute facts and constraints

Only call a fact or rule supplied/confirmed when it comes from an identifiable
user brief, answer or user-supplied model/data. Preserve that source alongside
its meaning and units; keep derived facts linked to their inputs and derivation.
A producer schema, example, preset default or capability limitation describes
the selected contract, not the user's requirements.

Keep unmentioned constraints unresolved. Ask whether a relevant limit applies;
do not infer either that it is required or that it does not exist. For example,
when the user has mentioned only orders and vans, a driver-hour limit or depot
return deadline is a possible rule to clarify. An inspected enforcement gap
should be conditional: “If you require a return deadline, this contract's
enforcement needs verification.” It must not appear under “supplied but not
enforced.” That label requires both an actual requested rule and an evidenced
enforcement gap.

When the user later requires an eight-hour duty limit or return by 16:00, carry
those exact requirements forward with their source and units. Keep any actual
enforcement gap visible before dependent execution. Do not promote other
example/preset constraints along with the confirmed ones.

## Path A: adapt a known pattern

1. Explain the structural fit and select the actual declared model/template.
   Reuse an existing customer model; catalog/demo names are starting examples.
2. Map supplied data to required fields/IDs/units. Resolve only material missing
   facts; read manifest clarification rules before assuming defaults.
3. Identify the model delta: changed parameter, new rule declaration, derived
   measure, objective aggregation or fixed commitment. Keep each business meaning
   linked to its applicable typed contract, input facts and hard/soft priority.
4. Author the candidate change in that producer's actual format. Preserve all
   requested semantics. A named preset missing a rule is not necessarily a
   missing primitive; compose available declarations before an extension handoff.
5. Validate the artifact and demonstrate a small valid and violating/boundary
   case for each material addition using the canonical evaluator. Expose
   registered-but-unevaluable or unpriced rules; do not claim enforcement.
6. Continue [validation/execution](inputs-and-execution.md) and
   [results/repair](results-and-repair.md). Move into Path B if the recipe cannot
   express the decisions; retain the completed work.

The [roster](patterns/scheduling-and-timetabling.md) and
[container](patterns/packing-and-consolidation.md) exercises illustrate deltas.
Their expected checks are not claims that a target contract has been validated.

## Path B: define a custom problem

Show the evolving model in the user's language before technical artifacts.
Ask in dependency order rather than demanding a fixed questionnaire.

1. Frame outcome, planning horizon, decision maker and allowed changes. Establish
   whether any feasible assignment suffices or an objective should rank plans.
2. Separate known facts from chosen variables. Define entities/resources,
   identities, domains, quantities, relations, sequence and time/resource shape.
   Do not rename a new business domain as vehicles or shifts to fit a demo.
3. Define rules, exceptions, totality/optional service and frozen commitments.
   Record source, meaning, scope, required data and checkable examples.
4. Define requested objective priorities, units, signs and aggregation/pooling.
   Preserve satisfaction-only intent; if an execution format needs an objective
   representation, explain and validate an equivalent neutral representation
   rather than inventing a business ranking or weights.
5. Map to available canonical contracts and compose a candidate manifest/model.
   Distinguish a missing name, missing data, invalid artifact, missing primitive
   and infeasible instance. Identify the precise unsupported semantics when
   lowering cannot preserve them; retain supported parts for the owner.
6. Establish a typed input contract through the selected canonical artifact:
   required fields, units, IDs, bounds, source/binding provenance and explicit
   derivations. Keep unresolved assumptions visible. No executable-looking
   placeholder schema or guessed field is a validated artifact.
7. Create labeled synthetic valid, boundary/violation and contradictory examples
   where meaningful. Validate schema, completeness, admission and actual rule/
   objective behavior; refine with the user instead of silently dropping rules.
8. With suitable data and authority, use the bounded execution path, inspect the
   final evidence, and refine quality or stability without changing requirements.
   Retain repair/what-if needs. Reuse/publication follows the supported lifecycle.

## Synthetic custom brief

A laboratory has one shared inspection chamber. Required tests T1 and T2 last
20 and 15 minutes; T2 starts at least 10 minutes after T1 ends. All times are
minutes from horizon start. Any feasible schedule suffices; there is no business
cost objective. In a fixture fixing T1 start to 0, T2 start 30 is the valid
boundary; start 25 violates the required gap. Occupancy must also be evaluated.

The candidate needs test/resource identities, duration inputs, interval/ordering
and shared-resource semantics plus the gap rule. Retrieve the target's schemas
and supported declarations, map each semantic item, author that actual artifact,
and run its validators/evaluator. If only unordered membership is available,
name missing interval/precedence/resource semantics instead of claiming a
verified schedule. This is a model-definition exercise, not a wire payload.

## Preserve UI with the model

Use [manifest UI](manifest-ui.md) when a model declares discovery, inputs,
controls, panels or view hints. Preserve compatible metadata, stable IDs and
versioned request/result bindings during both paths. Validate load/edit/save/
reload where supported; artifact validation alone does not prove rendering.

## Handoff artifact

Return the problem/decision summary, actual candidate artifact and typed inputs
when the format is established, rule/objective-to-contract-and-check mapping,
validation evidence, assumptions and unresolved gaps. When a contract is
missing, deliver the useful brief and exact needed contract, not a fake artifact.
Separate a successful private trial from registration/admission/activation;
see [lifecycle](lifecycle-and-feedback.md). A new combination of supported
primitives is ordinary modeling, not automatically core engineering work.
