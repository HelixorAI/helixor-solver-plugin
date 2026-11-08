# Reuse, outputs and feedback

## Keep lifecycle stages distinct

Configuring parameters of an existing admitted model, authoring an inline/private
candidate, registering a descriptor, validating/admitting a pack, activating a
version, retiring/rolling back and publishing a built-in release are different
operations. Establish each stage's actual contract and authority. Schema-valid
or registered does not mean admitted/active; a trial solve does not persist or
install its draft. A runtime implementation does not prove catalog operations
are exposed through the user's interface.

Reuse the canonical versioned pack/extension path when the user asks for reuse.
Retain the reviewed candidate, rules/objectives, typed inputs and validation
examples. If an essential primitive is absent, identify the owning shared
extension with its exact semantic gap. Do not create a parallel rule/model
store or publish a pack just to make a candidate executable.

## UI metadata across versions

Preserve compatible [manifest/UI declarations](manifest-ui.md) with adapted or
custom models. Trace stable field IDs and input/action/result bindings through
supported load/edit/save/reload. Detect stale cached metadata or dangling IDs;
keep selected UI build plus manifest/service versions with consumer evidence.

## Preserve provenance and comparisons

Retain input/source snapshot IDs, model/manifest/pack version, job/result ID,
actual engine/provider/device, options/seed, build/contract identity and budget
where the contract exposes them. Missing stamps limit comparability; a seed
alone is not a reproducibility proof. Explain a declared automatic engine
choice or report an unexplained mismatch; never silently substitute one.

Separate objective measures from service usage/cost. Carry verified invocation
context and required correlation/decision references, without inventing charges,
identity or publication grants. Keep output feedback linked to the actual run
through a supported store only when authorized.

## Present and use outputs

Show the plan with findings, stable record IDs, units and partial/failed states.
Use an available specialized table/timeline/map when supported; otherwise an
honest generic plan/findings table is useful. Verify export formats and access
before promising an export. Visualization metadata does not prove a renderer
exists, and an export is not permission for writeback, dispatch or publication.
For container plans, do not invent spatial coordinates from group membership.

Distinguish feedback types: wrong source facts, user edits, missing domain
meaning/contracts, solver quality and user acceptance. A user accepting a plan
is not independent feasibility evidence. Correction may need data validation;
a disruption may need [repair](results-and-repair.md#repair-an-existing-plan).
Record version-linked feedback only through supported authorized storage; do
not collect it automatically, create a private store or promote edits into
active rules/models/learned policy. Further lifecycle or operational actions
retain their own supported interfaces and user authority.
