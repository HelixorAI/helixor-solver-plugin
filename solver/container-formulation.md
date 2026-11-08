# Formulate container consolidation and loading problems

Use with [general formulation](formulation.md) and the
[packing and consolidation recipe](patterns/packing-and-consolidation.md) when
an LLM turns a cargo brief into a Helixor candidate. The LLM supplies faithful
inputs and required semantics; supported solvers and verifiers choose and check
allocations or placements. Follow [inputs and execution](inputs-and-execution.md)
for the actual invocation contract.

## Choose the intended decision

Separate cargo-to-container or container-to-sailing allocation from physical
2D/3D placement. Palletization, vessel stowage, yard positioning and empty
container repositioning can add different decisions. A family name or shared
word such as packing is not evidence that one contract handles them all.

Establish whether all cargo must ship, cargo may be selected, or quantities may
split. Mandatory indivisible consolidation is different from a knapsack that
may leave low-value cargo behind. Identify available physical containers,
container types and sailing slots separately. A type is not a promise of unlimited
inventory, and offering the same physical asset on several sailings does not
create independent available containers. Preserve any shared-asset/stock limit
through a supported declaration or name the gap.

## Provide source facts with the native contract

Give the LLM the exact brief, selected producer/model version, accepted payload
forms, declared input fields, rules, objectives and actual enforcement limits.
Use this table to check coverage; it is not another payload schema:

| Meaning | Preserve |
| --- | --- |
| Cargo identity | Order/line/item IDs, quantities, mandatory/optional status, split permission and any together/apart requirements |
| Size and mass | Per-piece versus shipment-total volume/weight, quantity basis, units, packaging/pallet contribution and stated uncertainty |
| Equipment | Actual IDs/types/counts, usable volume, allowed cargo payload, applicable gross/tare basis and compatibility |
| Sailing/slot | Destination and relevant origin, departure, arrival, cargo readiness, deadline and planning/time-zone conventions |
| Cost and preference | Per-used-slot versus per-shipment charges, fixed versus variable terms, currency/basis, priorities and objective sense |
| Physical loading | Usable internal dimensions, item dimensions, allowed rotations, containment/non-overlap, support/stack/load-bearing and access rules when requested |

Keep fields attached to their own stable ID through normalization and results.
Do not independently sort a volume column, merge equal-sized orders, or drop
zero-volume/zero-weight required cargo. Shared SKU or destination does not mean
two order lines are interchangeable. Preserve quantities and rounding rules.
If the source gives per-piece measurements, use the supported preparation path
to derive totals once, keeping the source basis; do not multiply an already
shipment-total value by quantity again.

When authoritative IDs are supplied, preserve them exactly and keep readable
labels separate. If the brief gives only names, establish how the selected
contract binds an internal identifier to that source name; do not present a
new identifier as a supplied fact. Role labels and canonical IDs can be
ambiguous in prose. Explicitly label or quote IDs in integration source records
rather than repairing generated names with a prefix-stripping parser.

## Keep capacity dimensions independent

A load can meet cubic capacity and exceed payload mass. Both limits bind per
used container; summing capacity across all equipment is not a placement rule.
An indivisible shipment exceeding every individual container cannot be split
implicitly merely because aggregate fleet capacity is sufficient.

Distinguish cargo payload from gross container weight and tare. When a source
states a gross allowance, use an established preparation/derivation contract to
account for supplied tare and other included mass; do not invent those values
or label gross capacity as usable cargo capacity. Keep kilograms, tonnes, cubic
metres and count units consistent. Uncertainty or safety margins require an
explicit supported model, not a guessed universal fill factor.

Missing capacity does not mean unbounded capacity. Missing cargo weight does
not mean zero. A declared required column is useful only when the actual
validation/admission path checks each supplied row. Inspect both the manifest
input contract and the rules' consumed attributes: a contract requiring only
that shipments and containers exist can still omit information needed by a
capacity rule or objective. Tighten domain requirements through the native
manifest/pack input contract where appropriate; do not write a private schema
or accept a scored candidate based on fewer source requirements.

## Model schedule and compatibility exactly

Keep readiness, departure, arrival and required delivery distinct. Cargo cannot
use a sailing that leaves before its permitted ready time; its arrival must
satisfy the requested deadline. A departure before the deadline alone does not
establish timely delivery. Preserve boundary inclusivity and declared calendars,
cutoffs or transit legs where they matter; never invent a time-zone conversion.

Destination compatibility, customer partitioning, temperature/segregation and
other supplied requirements need their own supported contracts. Do not replace
a hard compatibility rule with a soft preference. When a booking model requires
one common candidate sailing for all co-loaded bookings, check the whole set
intersection. Pairwise intersections are insufficient: {1,2}, {2,3}, {1,3}
overlap in pairs but have no element common to all three. Different candidate
sets are not necessarily incompatible either. Use that rule only where the
selected model actually declares and evaluates it.

Which container or sailing to choose is a solver decision. Ready dates, travel
schedules and a required capacity/cost value are inputs when the selected goal
needs them. Keep genuinely unknown facts absent or explicitly unknown according
to the native contract, retaining all other facts and rows. Clarify an ambiguous
unit, date meaning or quantity basis; do not fabricate a feasible interpretation.

## Preserve the requested objective

A cost charged once per used container/slot is not charged once per shipment.
Verify the grouping key and objective term against actual supplied rates.
Minimizing container count, freight cost and unused space can rank different
plans. A weighted sum is not automatically a lexicographic priority or a
feasibility-only goal. Preserve the source's ranking, weights and hard/soft
meaning in the supported artifact; do not inherit example weights as user facts.

Minimum fill may be a soft preference or a hard dispatch requirement. Establish
which, whether it applies only to occupied containers, and what a shortfall
means. A higher fill ratio cannot justify omitting mandatory cargo. Report its
denominator: used capacity versus all available capacity are different measures.

## Physical fit needs separate evidence

Volume11 can be less than container volume250 while an11x1x1 box cannot fit
orthogonally inside a10x5x5 space. Aggregate weight/volume admission does not
check dimensions, rotation, overlap, support, stability, stacking, door access,
unloading order or weight distribution. Do not infer any of these from an
allocation certificate or a three-dimensional-looking diagram.

When physical loading is requested, establish usable internal dimensions,
allowed orientations and each required physical rule, then trace them to actual
placement variables, execution and verifier coverage. A container assignment
cannot stand in for coordinates/rotation/support evidence. A missing geometric
or stability primitive blocks the full loading claim; retain the useful
allocation brief and name the exact unsupported requirement.

## Check formulation and result separately

1. Map every required cargo row, equipment option, capacity, schedule rule and
   goal to its actual candidate representation and source. Preserve explicit
   missing facts and unsupported requirements.
2. Validate the native input contract, including every supplied row. Check
   required rule/objective attributes and actual enforcement before execution.
   A permissive request envelope or entity-presence check alone is insufficient.
3. Execute only the authorized source-faithful supported problem. Never add
   containers, reduce weight, split cargo, change dates or suppress a rule to
   make an infeasible stated instance look solvable.
4. Read actual cargo coverage/IDs, used slots, loads, schedule/compatibility
   checks, objective components, shortfalls and unevaluated rules. An infeasible
   candidate or search failure is not by itself a global impossibility proof.
5. State whether evidence establishes aggregate allocation, physical placement
   or only a partial result. Feasibility is not global optimality, transport
   safety certification or permission to book/dispatch cargo.

For generation evaluations, freeze source-equivalence rules before inference.
Report literal request agreement separately from ID-preserving row reordering
and native-supported null/absent representations of genuinely unknown facts.
Those comparison views must never modify the executed model output. Include
independent capacity failures, schedule/port conflicts and partially missing
rows; keep geometry probes separate. Preserve raw failures and qualification
limits rather than tuning repeatedly on cases described as unseen.
