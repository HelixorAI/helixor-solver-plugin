# Pattern recipes

Choose by decisions and relationships, not a fixed catalog name. Confirm the
selected target's canonical model/template, input contract and admitted version.
These recipes teach modeling structures; they do not assert deployment support.
Keep family, formulation, method and evidence [distinct](terminology.md).

| Starting structure | Recipe |
| --- | --- |
| Vehicles/technicians visiting jobs, possibly with production coupling | [Routing and scheduling](patterns/routing-and-scheduling.md) |
| People/shifts, classes/resources, machine operations or project activities | [Scheduling and timetabling](patterns/scheduling-and-timetabling.md) |
| Cargo assigned to containers, physical placement or palletization | [Packing and consolidation](patterns/packing-and-consolidation.md) |
| Jobs/resources, networks/facilities, inventory, fulfillment, batching or bookings | [Allocation and inventory](patterns/allocation-and-inventory.md) |

Each recipe identifies facts, common rules and objectives, a synthetic example
and verification limits. Use [Path A](modeling.md#path-a-adapt-a-known-pattern)
for a structural fit plus supported additions. For a hybrid/new structure,
carry established facts into [Path B](modeling.md#path-b-define-a-custom-problem).
Do not demand a named preset or a new engine solely because vocabulary differs.

A normal worked example must retain its selected canonical artifact and actual
validation/evaluation result before it becomes an executable example. The
examples here are domain-level exercises, not wire payloads or claimed runs.
Never substitute them for missing customer data. Use a target-released template
when available and disclose any exact primitive that cannot preserve a rule.
