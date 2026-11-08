# Translate a routing brief into a solver problem

Use with [general formulation guidance](formulation.md) and the
[routing recipe](patterns/routing-and-scheduling.md) when an LLM prepares a VRP
candidate. The LLM's output is the routing problem, not the routes or a claimed
solution. The selected native validator, optimizer and route verifier own those
steps. Use [inputs and execution](inputs-and-execution.md) for invocation.

## Establish the exact routing scope

Start from supplied requirements and the target's discovered input and
constraint contracts. Identify required visits, allowed vehicles, depots,
load dimensions, travel model and requested ranking. Reuse known facts;
clarify only decisions that change the model. The label VRP does not decide
whether vehicles return, deliveries may split, visits are optional, roads are
directed, or time windows and driver-duty limits apply.

A useful first scope is homogeneous vehicles, one depot, one closed route per
used vehicle, nonnegative delivery demands, mandatory indivisible visits and
a specified distance objective. Use it only when it matches the actual brief.
Extra pickup, timing, skills, heterogeneous capacity or cost requirements must
remain visible and map to supported declarations; do not squeeze them into
this simpler scope or silently remove them.

## Supply a readable formulation brief with the native contract

Give the LLM the exact source plus producer/version-specific input description,
accepted payload forms, schema, supported constraint/enforcement metadata and
required goal. Where supported, retain source provenance with each entity and
rule. This is a review checklist, not a new wire format:

| Source meaning | Preserve in the candidate |
| --- | --- |
| Visits/orders | Stable IDs, every required visit and its own location, demand and service data; distinct customers may share a location |
| Depot and route endpoints | Explicit start/end locations and allowed depot assignments; return/open-route meaning and any separately required return deadline |
| Available fleet | Count or actual vehicle records, per-vehicle capacities, availability and compatibility; a limit on available vehicles is not a requirement to use them all |
| Load | Demand and capacity in matching dimensions/units, delivery versus pickup signs, and permitted split/reload behavior |
| Travel | Coordinate system/order, metric, units, directed distance/time matrix and row-ID binding when the contract supports it; provider/version/snapshot when relevant |
| Time requirements | Service duration, availability, departure horizon, window anchor, waiting policy and hard versus penalized meaning |
| Goal | Requested distance/time/cost/service ranking, priorities and penalties; feasibility-only remains feasibility-only |

Use the selected contract's actual field names, not names invented from this
table. Keep all parallel arrays and matrices aligned to the same node mapping;
include the depot exactly where that format requires it. Preserve an ID-to-node
map through normalization and returned routes. Sorting names, coordinates or
demands independently changes the problem. Never merge co-located visits or
drop zero-demand visits unless the source explicitly permits it. Zero is a
value, not missing data.

A route assignment and visit order are solver decisions. The LLM need not
know them to produce complete inputs. Available fleet size, load capacity or
a required customer's missing location are different: preserve the gap and
use the supported missing-input/clarification path. A placeholder coordinate,
guessed capacity or extra vehicle fabricates an easier instance.

## Keep metric and units faithful

Planar Euclidean coordinates measure distance in their coordinate units;
latitude/longitude with great-circle distance measures another geometry.
Neither is automatically a road-network distance or travel time. Preserve the
requested matrix/provider path where supported; do not substitute straight
lines, a default speed or live-traffic claims without source and capability
support. Distance and duration matrices can be asymmetric; do not symmetrize
them or reorder their IDs independently.

Mixed load dimensions need corresponding capacity dimensions. Kilograms,
parcels, pallets and vehicle counts cannot be added together. Apply only
source-backed, dimensionally valid conversions supported by the contract,
retaining original values and derivation evidence where applicable. An
unmentioned service time or speed default describes the producer, not a
customer-supplied fact; establish whether it affects required semantics. Missing demand also needs an
explicit interpretation: do not silently turn it into unit demand unless the
source or selected model permits that convention.

## Model relationships before deciding feasibility

Each mandatory visit needs exactly-once coverage; selected vehicle routes need
valid endpoint/flow and connectivity semantics. Use the canonical model and
constraint evaluators to express these. Degree or assignment constraints alone
do not prove a connected depot route. Do not implement a second optimizer,
subtour handler or English parser in the application.

Capacity is per vehicle along its route under the actual load semantics.
Total demand no greater than fleet capacity is only a necessary check for
indivisible deliveries: a single demand can exceed every vehicle's capacity,
or the demands may not pack into the available vehicles. Preserve stated
infeasibility. Do not increase capacity, add vehicles, split/drop deliveries
or insert reloads to make the source problem solvable.

For timing, distinguish arrival, service start, service completion and departure.
When waiting is allowed, service starts after both arrival and the opening
bound; the next arrival includes the previous service duration and travel.
An arrival-window, start-window and completion-window are different rules.
Match the producer's hour/minute and time-zone conventions explicitly. A
return-to-depot rule is not a depot-return deadline or a driver-duty limit.
Pickups/deliveries additionally need supported pairing, precedence, same-vehicle
and intermediate-load semantics; final net load alone is insufficient.

These are modeling obligations, not claims that every engine supports them.
Trace required rules to actual construction and final verification coverage.
A manifest declaration, JSON field, imported engine or pre-solve reachability
check does not establish enforcement on the final route. Preserve unsupported
requirements as blockers to a full-problem solve. Read the result's unchecked
or not-enforced rules and the exact certificate scope.

## Example: structured inputs before routes

A source says: depot [0,0]; at most two identical vehicles, each carrying
7 crates; Orin at [3,0] needs 2 crates, Pella at [0,4] needs 5, and Soren at
[6,0] needs 3. All visits are mandatory and indivisible, routes return to the
depot, and total planar Euclidean distance is minimized. No time requirements
are supplied in this example.

The candidate must preserve all three ID/location/demand bindings, depot,
available count, capacity per vehicle, metric and objective. Which vehicle
serves each visit and the visit order remain unknown decisions. Missing
route order is not a missing input. Use the actual producer's accepted payload
and validator; this brief is not an execution receipt or universal request
schema. Do not turn it into a time-window or driver-hours model by default.

## Verify translation separately from route quality

1. Check source coverage and bindings: no omitted visits, changed demands,
   invented parameters, weakened required rules or altered objective.
2. Validate the native request and input semantics. A permissive outer request
   schema can accept a problem map that the native validator must reject.
3. Establish that every required rule can be executed and checked on the
   selected target. A capability gap is different from missing customer data.
4. Run the authorized bounded solve, then inspect actual visit coverage, loads,
   endpoints, route timing and unchecked rules within the certificate's scope.
5. Report feasibility and objective evidence separately. A feasible route is
   not proof of global optimality, and a better cost on a changed problem is
   not improved translation.

For a local LLM comparison, freeze the contract, original model, prompt
conditions, budgets and new cases before inference. Include reordered IDs,
zero/decimal loads, co-located distinct visits, genuinely missing inputs and
stated infeasibility. Never supply reference payloads or solutions to the
model, repair its outputs silently or reuse cases as unseen. Report exact
payload agreement separately from reviewed equivalent representations and
native solve outcomes. Initial synthetic CVRP results do not qualify richer
VRP variants, customer deployments or installed-host behavior.
