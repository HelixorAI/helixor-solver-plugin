# Allocation, inventory and related patterns

Use [terminology](../terminology.md) for sourced names, variants and distinctions.

## Match structure before a catalog label

| Pattern | Decisions, inputs and common changes |
| --- | --- |
| Assignment/matching/GAP | Associate tasks and resources; cardinality, capacities, eligibility and agent-dependent consumption/cost. Clarify unmatched demand |
| Network/transport/facility planning | Paths/flows, intermediate locations, supplies/demands and capacities; facility opening decisions differ from fixed-site allocation |
| Inventory/fulfillment | Quantities, stock balance, demand, lead times, supply and service dates; lot sizing/replenishment adds horizon decisions |
| Batching/grouping | Compatible work shares capacity/setup/cost; distinguish per-item, per-group and whole-pool pricing |
| Reservations/bookings | Assign bookings to resources/time intervals with capacity, compatibility, overlap and reassignment rules |

Use a target-declared model/template and preserve units, totality, sequence and
time/resource coupling. Network flow is not automatically indivisible job
assignment; grouping orders is not a pick/processing sequence. Fixed readiness
is an input; jointly choosing production and delivery requires a composed model.

## Synthetic examples and adaptation

For allocation, demands D1=3 and D2=4 share supply capacity 6 in the same unit.
Serving both fully from that supply cannot pass capacity validation (7>6).
If unmet demand is allowed, it must be reported and priced/ranked under the
actual model; otherwise a partial allocation is not a successful full solution.

For batching, orders A and B share departure G. A user-provided rule charges a
setup once per used departure. Two orders in G incur one setup, not two.
A whole-pool rate over several departures is a different aggregation and must
have its own preserved contract; never invent a multiplier or treat missing
numeric facts as zero.

For reservations, bookings X and Y each require the same indivisible room
from minute 10 to 20. Both cannot be placed there together under a hard
non-overlap rule. Moving one requires an available permitted alternative,
not a fabricated capacity increase. Use valid/violating examples for the
customer's adaptation and preserve an existing reservation baseline for repair.

## Verification and interpretation

Check balance, capacity, required service, aggregation and timing through the
selected canonical model/evaluator. Inventory Routing Problem couples stock
and routes; Production Routing Problem adds production decisions. Map their
coupling explicitly using [custom modeling](../modeling.md#path-b-define-a-custom-problem).
Do not turn a forecast or historical quantile into certain inventory or a joint
service guarantee. Explain quantities, unmet demand and comparison assumptions
through [results](../results-and-repair.md).
