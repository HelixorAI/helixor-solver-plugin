# Results, evidence and repair

## Read the actual result

Separate execution state from model verdict. A finished call or all-zero score
bands alone does not prove feasibility. Use returned certificate/assessment,
evaluated-rule coverage, violations and shortfalls. Describe feasible, proven
infeasible, unbounded, pending/unresolved, unverified and failed states only as
the producer establishes them. No candidate in budget is not a global proof.

Explain the plan alongside the certificate: required versus optional placement,
served/unserved quantities, hard violations, soft preferences and objective.
Legal unplaced work still leaves demand unmet. Missing placement evidence is
not zero unmet demand; an empty accepted plan is not automatically full service.

Read the actual score priorities/bands, signs, units, weights, count versus
magnitude and denominator. Do not assume every service uses a public example's
band names or scoring formula. A per-group cost is not a whole-pool cost;
missing measures or invalid expressions cannot silently become zero.
Identify rules declared, schema-valid, admitted, evaluated and priced during
search separately. A certificate covers its evaluated model and facts, not
unknown rules, operational reliability or legal compliance beyond that scope.

Use [evidence terms](terminology.md#evidence) for incumbents, bounds/gaps,
tolerances, slack, dual/sensitivity and conflict/IIS distinctions. Never infer
these fields from a generic certificate. Preserve unknown travel/readiness,
resource dependencies and uncertainty assumptions. A marginal historical
quantile does not establish a joint probability guarantee.

Show a supported table/timeline/map/export using stable IDs and units. If the
specialized view is absent, present a generic plan/findings table. Do not invent
coordinates, geometry, timelines or writeback from UI metadata. Explain actual
engine/version/provider/device and comparison limits where returned; no guessed
speed, reproducibility, minimum-change or optimality guarantee.

## Declared views and repair controls

Use [manifest UI](manifest-ui.md) to distinguish declared panels/nested fields
from actual consumers and request/result bindings. An absent renderer can use
an adequate existing generic view; a required missing binding is an explicit
gap. Visible controls never prove frozen commitments are enforced.

## Repair an existing plan

1. Identify the real baseline, entity mapping, representation and version,
   changed facts/disruption and governing model. Matrix and grouped-index
   forms are not interchangeable without the producer's supported conversion.
2. Establish completed/frozen assignments, mutable scope, change limits and
   stability preferences. Verify enforceable controls on this exact model,
   release and interface. A search budget is not an assignment-change limit.
3. Select the actual repair operation/options. A warm start is not automatically
   repair; a request's input-correction hint is not a plan-repair operation.
   Do not invent `solver.repair` or silently replace repair with a new solve.
4. Validate baseline shape/IDs, pins, new facts and controls. A frozen assignment
   conflicting with a new hard restriction is a conflict to explain, not an
   instruction to unpin, alter facts or soften a rule. Unsupported mandatory
   preservation blocks dependent execution.
5. Run the supported operation within existing authorization and budget. Use
   the same canonical validation/admission/evaluation path; preserve the baseline
   as history. Do not edit source systems or apply the result implicitly.
6. Compare actual before/after evidence: changed assignments, enforceably
   preserved commitments, unmet demand/violations, comparable objective and any
   unreported deltas. Recheck the old baseline against changed facts before
   offering it as valid. A withheld illegal candidate is not a successful repair.
7. Explain verified repair, unchanged valid plan, remaining inadmissibility or
   no verified candidate in budget. Offer supported scope/budget/relaxation
   choices without automatically escalating. Minimal change needs its own
   objective and evidence; stability preference alone is not a guarantee.

## Select the right change

| User intention | Distinction |
| --- | --- |
| Fix malformed input | Input correction, followed by applicable validation |
| Restore an existing plan after disruption | Baseline-aware repair with protected commitments |
| Improve preferences on a valid baseline | Re-optimization/polishing; changes may be broader |
| Compare different facts | Labeled what-if run against an identified baseline, without live fact changes |
| Relax a hard rule | A changed problem requiring the user's authority; never a silent repair step |
| Recover a failed or lost job | Execution/retrieval recovery under [the interface contract](inputs-and-execution.md), separate from planning |

Synthetic repair exercise: baseline has A→S1 frozen; new data makes A unavailable
for S1. Both requirements cannot be silently met by keeping A or reassigning
S1. Expose the conflict. If a legal alternative is authorized later, validate
that changed scope before repair. No example here claims an actual service run.
