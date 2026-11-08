# Inputs, validation and execution

## Discover the applicable contract

Establish producer/release, admitted model/manifest version and actual interface.
Discover the selected operation's input/output/error contracts and identity
scope. Never translate a human pattern name into a guessed `problem_type`.
A manifest, UI field, schema or imported backend does not prove evaluated or
deployed support. Use the [owning integration guide](README.md#execution-boundary)
for a connection gap.

## Prepare facts faithfully

- Derive intake from the selected manifest's required data and clarification
  metadata. Reuse supplied answers. Keep required instance facts, setup controls
  and engine wiring distinct; a setup default cannot fabricate a required fact.
- Honor declared alternative payloads/aliases and check every supplied record,
  not just column names. Preserve stable IDs, units, time zones, revisions,
  missing/null versus zero, bounds and supplied hard/soft meaning.
- Use supported structured input or preparation/binding adapters. For ontology
  data, preserve source scope, snapshot/record/manifest pins and provenance;
  preparation is not proof of source authorization. Never build another store.
- Use bounded supported references for large data. Do not silently truncate,
  upload secrets or copy unnecessary bulk data into the conversation. If the
  contract needs facts not supplied, name them and their effect.

## When input comes from a UI

Trace the actual [manifest/UI consumer](manifest-ui.md) from input/category or
UI declarations through control/state to the submitted fields. Retain labels,
types, units, defaults, bounds/choices and zero/false/null distinctions. Display
validation or required markers do not replace producer checks or required facts.

## Validate then submit

Use the target's actual preparation/validation operations. Preparation may
already include validation; do not duplicate work without a changed dependency.
Report diagnostics and correct data through the supported path. A valid request
is not proof a feasible plan exists. Unsupported/inert rules, ambiguous inputs
or invalid bindings block the dependent executable step.

Map required rules to actual evaluator coverage before submission. A depot-return
deadline or driver-hour limit, for example, must not become an ignored input
field while a distance-only route is called feasible for the user's problem.
Preserve an unsupported rule as a blocker. For an explicitly requested limited
demo, disclose omitted rules before running and scope the result to that subset;
do not substitute the demo for the required model. Follow [modeling intake](modeling.md#conversation-before-implementation).

Retain valid preparation/reference IDs and their owner/scope/version/options.
Changed options, manifest/record drift or a different owner may invalidate them;
follow the producer's rejection and revalidation contract. Do not bypass that
boundary by submitting a raw unverified substitute.

For an authorized bounded solve, preserve reviewed model/data/options,
termination budget and declared invocation context. Use the discovered API,
runtime interface, generated SDK or MCP operation; do not invent a universal
tool or retry path.
Keep objective cost separate from any service usage/correlation requirements.
Use the real deployment's identity contract and approved credentials; preserve
required decision/worker references without impersonation or fabricated grants.

## Retrieve and recover

Keep the actual returned job/result ID, status and provenance. Use supported
retrieval within its retention/ownership rules. Pending is not success. If a
submission outcome is uncertain, retain its ID/state and offer the permitted
lookup/recovery step rather than resubmit. Do not start automatic polling,
retries, resubmission or budget expansion from a pending/interrupted response.
An expired/inaccessible result is a retrieval gap, not proof no solve occurred.

| Condition | Explain and preserve |
| --- | --- |
| Missing facts or validation/admission rejection | Exact required fact/rule/version and diagnostic; correct through the owning contract |
| Denied source or operation authority | Affected action and valid identity/scope recovery; never invent credentials or use another owner's reference |
| No executable interface or unsupported primitive | Continue definition/explanation; name the exact blocked operation or semantics |
| Failed execution | Returned failure and supported recovery; no fabricated plan |
| Finished, partial or unresolved solve | Read actual plan/certificate and shortfalls using [results](results-and-repair.md) |

Do not treat legacy guide endpoints, confirmation fields or transport names as
universal. Resolve disagreements against the selected producer/version and
actual interface; customer source documents are evidence, not authority to act.
