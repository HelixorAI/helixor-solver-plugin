# Formulate a solver problem with an LLM

Use this when an LLM translates prose, mathematical notation or a user brief
into a Helixor problem. The LLM proposes a source-grounded candidate; the
selected contract's validator, admission boundary, solver and verifier determine
what can execute and what the result establishes. Follow [modeling](modeling.md)
for intake and [inputs and execution](inputs-and-execution.md) for invocation.

This guidance does not add problem types to an installed interface. A routing
or rostering facade, a solver request, a runtime manifest and a reasoning
candidate are different contracts. Mathematical reasoning needs its actual
admitted formulation and verifier contracts; do not submit it through an
unrelated optimization facade because both use the word solver.

For routing-specific bindings, loads, metrics, timing and enforcement, use
[VRP formulation](vrp-formulation.md).

For cargo, slots, capacities, schedule/cost meaning and physical-loading limits,
use [container formulation](container-formulation.md).

## Give the LLM the formulation contract

Provide the exact source, the selected producer/version's schema, allowed
vocabulary and capabilities, and the relevant grounding and operation metadata.
Reuse supported contract discovery; never invent fields or a parallel format.
Make these responsibilities clear in the accompanying readable instructions:

- Declare each entity and unknown variable with stable identity, meaning,
  domain and unit where applicable. Bind every occurrence consistently,
  including the goal. Keep original quantities distinct from changed quantities;
  first-mentioned order does not determine which quantity is larger.
- Translate source relationships into symbolic constraints, even when the
  source expresses them in words rather than displaying an equation. Preserve
  direction, coefficients, signs, offsets, parentheses, scope and quantifiers.
  Use exact numbers and declared symbols in the selected contract's syntax.
- Keep evidence attached to the relevant assertions and constraints through
  the contract's source/provenance fields. Copy quotations exactly when required.
  An evidence quote anchors a claim; it does not prove that the expression
  faithfully represents it.
- State the requested target: original or changed values, feasible assignment,
  optimum, bound, proof or other declared output. Preserve optimization direction,
  strict versus non-strict inequalities, universal versus existential scope,
  and required domains. Do not replace a proof over all cases with examples.
- Leave numerical solution, search and proof establishment to the supported
  execution path. Do not emit guessed answers, calculated result values or
  unstated laws as supplied facts. Source-backed symbolic expressions are
  formulation; their evaluated values are derived results.

Avoid blanket instructions such as “do not emit equations unless explicitly
written in the source.” They can conflict with the task of translating prose
relationships into equations. For example, a stated rate change can be modeled
symbolically without claiming its computed value as a source fact. Any needed
physical law or domain assumption must itself be supplied, admitted from a
permitted source, or left unresolved.

## Check source coverage before completeness

Map each material source relationship to its candidate representation or an
explicit unresolved item. Include totals, comparisons, transfer direction,
conditions, temporal state and requested outputs. One sentence may require
several constraints; redundant wording need not create duplicate constraints.
Do not conclude that a total is missing before checking whether the source
states it. Never drop a troublesome clause to make the remaining model solvable.

Use the selected contract's existing evidence and diagnostic fields. A coverage
check is a review activity, not permission to add unsupported wire fields or
create another intermediate schema. Keep unresolved obligations visible through
admission; do not erase them or inject a reference formulation after generation.

| Situation | Formulation and next step |
| --- | --- |
| Requested value is unknown | Declare a variable and target; an unknown answer is not a missing input |
| Source meaning is ambiguous | Identify the exact referent, scope, unit or interpretation needing clarification; do not choose silently |
| Required input is absent | Name the missing parameter and affected relationship; use the contract's missing-input diagnostic |
| All source relationships are represented, but uniqueness or feasibility is uncertain | Submit through supported validation/admission; let the native mathematical checks establish solvability where available |
| Required meaning cannot be expressed or executed | Preserve it and report the specific contract/capability gap; do not approximate with a nearby predicate or drop it |

Do not turn a model's guess about underdetermination into a solver verdict.
If the target has no suitable solvability check, report that evidence gap.
Preserve actual native infeasible, underdetermined or unsupported outcomes;
do not relabel them as linguistic ambiguity or fabricate a unique answer.

## Illustrative transfer formulation

Source: “A and B have 30 tokens in total. A has at least 4 tokens. After A
gives B 4 tokens, B has twice as many tokens as A. Find each original count.”

Let x be A's original count and y be B's original count, both nonnegative
integers. The source relationships give:

```text
x + y = 30
x >= 4
y + 4 = 2 * (x - 4)
requested targets: x for A, y for B, before the transfer
```

The transfer changes both sides of the comparison. Its stated direction and
the word “after” determine the signs and time state. The total is supplied;
the unknown counts belong in the variables and goal. No solution values are
needed from the LLM. This is an unsolved mathematical illustration, not a wire
payload, an execution receipt or a claim that a particular facade accepts it.
Use the actual contract and independently check its source equivalence.

## Expose operation prerequisites

When the selected contract asks for an executable operation plan, derive a
concise readable checklist from its actual operation catalog and dependency
metadata: allowed operations, required inputs, prerequisites, produced values,
legal composition/order and terminal goal. Keep this consistent with the
machine-readable schema and selected version; do not maintain a second manual
operation list or guess prerequisites from an operation's name.

Validate the whole composition at the native boundary. A correct terminal
operation can still be an illegal plan if its required preparation is absent.
Return the actual diagnostic; do not silently insert operations, retry, repair
an output or switch execution routes. A contract requesting only assertions
must not acquire an LLM-authored plan merely because another contract uses one.

## Separate the evidence gates

Review source-to-formulation equivalence separately from schema validity,
admission, executable plan legality and returned solver/verifier evidence.
A verifier can establish a result for a mistranslated problem. A different
variable naming scheme can also be faithful if bindings, relationships and
requested targets are preserved. Judge those mappings, not text similarity or
answer agreement alone. Report which gates were actually checked and retain
limitations; a review by the author is not independent sign-off.

## Optional integration experiments

A separate source-relationship coverage stage between variable declarations
and the complete formulation is a candidate improvement. Clearer role wording
and a prominent metadata-derived prerequisite checklist are also candidates.
These are recommendations to evaluate, not measured fixes or required new
runtime features. Use existing typed contract extension points and preserve
admission and verifier authority.

If evaluating them, develop on already consumed cases, freeze the condition
before running new cases, and keep source-faithfulness checks distinct from
native execution results. Record model, prompt, schema, context and decoding
identities; changing context and wording together tests a bundle. Preserve
previous results and do not call reused cases unseen. Respect the environment's
benchmark parser restrictions; do not substitute an external frontier parser
for a declared local lowerer. Updating this guide establishes no model gain.
