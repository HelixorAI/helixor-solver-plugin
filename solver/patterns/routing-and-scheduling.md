# Routing and scheduling

Use [terminology](../terminology.md) for sourced names, variants and distinctions.

For LLM-generated solver inputs, read [VRP formulation](../vrp-formulation.md)
for source coverage, node/ID alignment, load and travel semantics, and checks
that separate translation fidelity from route feasibility.

## Structure and intake

Assign visits to vehicles/people, order them and model travel/service timing.
VRP, VRSP, VRPTW and field-service/TRSP descriptions can overlap; do not map them
to a single guessed identifier. Use the target's actual routing/combined model,
not a membership-only assignment template.

Retain stable visit/resource IDs, depots, travel times/costs and units, service
durations, quantities/capacities, availability, windows and commitments. Ask
whether windows apply to arrival, service start or completion; whether waiting
is allowed; and whether bounds are hard or penalized only where still unknown.
Do not infer live traffic, breaks, labor rules or skills from the acronym.

For a vague delivery brief, establish applicable departure/return requirements,
driver-duty limits, required versus optional visits and distance/time/cost/service
priorities as well as the data above. Ask only unanswered questions; do not
turn an unknown rule into a preset default. Carry each required rule into the
canonical manifest and its evaluated checks before building a planner wrapper.

Typical additions include paired pickup/delivery precedence, multiple depots,
qualification/compatibility, synchronized teams and shared resources. Objectives
may trade distance, cost, lateness, unserved work and stability under declared
priorities. Required visits cannot disappear merely to shorten a route.

## Synthetic adaptation

Two visits A then B use one vehicle. At A, service starts at minute 10 and lasts
5 minutes; travel A→B takes 10 minutes. Arrival at B is minute 25. If B's hard
window is service-start 25–30 and waiting is allowed, a start at 25 is a valid
boundary example; 31 violates the requested window. These are arithmetic
expectations for the model check, not a service result.

Adapt the starting model through [Path A](../modeling.md#path-a-adapt-a-known-pattern):
map durations, travel and the exact window anchor to supported declarations.
Check the boundary/violation and evaluate the final route. A finish-window
contract is not silently equivalent to a start-window requirement.

If a manufacturing timeline is involved, distinguish fixed release/ready times
from machines/batches/production completion times chosen jointly with routing.
The latter calls for a composed/custom model (IPDS/production routing as
applicable), preserving resource and departure coupling through shared contracts.

## Results and changes

Report visit coverage, actual order/times and violated/unevaluated rules from
returned evidence. A cost or assignment list alone does not prove timing.
For a missed vehicle or delayed job, identify the baseline, completed/frozen
visits and permissible resequencing, then follow [repair](../results-and-repair.md#repair-an-existing-plan).
Compare what-if travel/readiness changes without altering source data or
claiming a stochastic guarantee from one scenario.
