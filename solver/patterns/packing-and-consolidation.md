# Containers, packing and consolidation

Use [terminology](../terminology.md) for sourced names, variants and distinctions.

For LLM-generated input candidates, read [container formulation](../container-formulation.md)
for source/ID/unit binding, required-field contracts, sailing/cost semantics
and separate allocation-versus-placement evidence.

## Establish the actual loading problem

Distinguish shipment-to-container/voyage allocation from spatial placement:
weight/volume capacity is not 2D/3D geometry. Palletization may include footprint,
layers and stacking. Container repositioning, yard location or vessel stowage
adds other decisions; do not silently include them in a packing recipe.

Establish single/multiple containers, available types/counts and whether all
cargo must ship, a subset may be selected or quantities may split. Required
all-item bin packing differs from selecting valuable cargo in a fixed space.
A high fill rate is not a substitute for required cargo coverage.

| Scope | Required facts/rules to establish |
| --- | --- |
| Consolidation | Item quantities, weight/volume and units; independent capacities, compatibility, container availability, readiness, departures/destinations and due dates if relevant |
| Physical placement | Usable internal and item dimensions; allowed orientations; containment/non-overlap; requested stackability, fragility/load-bearing, support and weight distribution |
| Loading operations | Access/door restrictions, loading/unloading order, completed/loaded commitments and permitted movement; supplied segregation/temperature rules when relevant |

Distinguish payload from gross/tare limits. Do not invent physical properties,
transport rules or available equipment. Confirm objective priorities: fewer
containers, freight cost, unused space, loaded value, service or repacking.
Use only a selected contract that preserves the requested semantics. An exact
missing geometry/stability/access primitive remains a gap, not a reason to
replace physical fit with an aggregate approximation.

## Synthetic fixtures

A container has volume limit 10 and weight limit 10. Item A has volume 6,
weight 4; B has volume 4, weight 7. All quantities are abstract consistent units
for this exercise. Together they meet volume but exceed weight (11); separate
containers with those limits can satisfy both capacities. This is a declared
check expectation, not a returned plan. Removing B is invalid if all cargo is
required, regardless of utilization improvement.

For physical fit, usable internal size is 10×5×5 length units; an indivisible
11×1×1 box cannot fit in any orthogonal orientation, despite its volume being
below 250. Do not invent permission to rotate, split or deform it. For fragile
cargo or delivery-order access, add separate violation fixtures: permitted
volume alone cannot verify those properties.

Use the selected canonical packing/consolidation artifact and [modeling](../modeling.md)
workflow for each rule. The domain tables here are not a new request schema.
Validate the model, then evaluate boundary/violation examples through the
owning verifier before executing an operational solve.

## Explain and repack

Show contents, loaded/unloaded quantities, container count, cost basis and used
capacity with its denominator (used containers versus all available containers
can give different fill rates). Only show coordinates, rotations, loading order
or a physical placement diagram when the result actually provides that data
and the relevant evaluation evidence. An assignment certificate alone is not a
geometric/stability proof or a safe-transport/optimality guarantee.

For repacking, use [repair](../results-and-repair.md#repair-an-existing-plan):
identify already loaded cargo and any frozen positions, preserve only controls
the actual model can enforce, explain movement and unresolved constraints, and
never claim pinning group membership preserves a physical location.
