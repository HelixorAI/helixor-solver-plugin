# Scheduling and timetabling

Use [terminology](../terminology.md) for sourced names, variants and distinctions.

## Select the decision shape

| Structure | Facts and material rules | Possible objectives |
| --- | --- | --- |
| Staff rostering | People, shifts/durations, skills, availability, coverage and fixed commitments; hours/rest and succession rules supplied by the user | Coverage priorities, fairness/preferences, staffing cost and stability |
| Class/resource timetable | Activities, allowed slots, rooms/equipment and attendance conflicts; capacity, overlap and adjacency | Compactness, preferences and resource use |
| Job shop | Jobs with ordered operations, durations and eligible machines; precedence and machine occupancy | Makespan, tardiness and setup cost |
| Resource-constrained project scheduling (RCPSP) | Activities, dependencies and resource requirements/capacities; modes/skills if decisions | Completion span, resource cost and service priorities |

Use the matching declared model or compose available contracts. Membership
alone cannot enforce ordered operations or time-overlap constraints. Distinguish
mandatory coverage from legally optional unplaced work; keep required instance
facts separate from model setup defaults.

## Synthetic roster adaptation

Shift S1 lasts 4 hours. Workers A and B are qualified; A is unavailable for S1,
B is available and has a 4-hour remaining cap. Exactly one worker is required.
An assignment B→S1 is the valid fixture; A→S1 violates availability; leaving S1
empty violates required coverage. A new customer cap must be mapped to the
canonical constraint and evaluated, not just mentioned in prose.

Do not invent legal rest/hours limits or default skill equivalence. Obtain the
applicable user rules, units, time zone and horizon. A fairness preference must
not weaken eligibility or a hard coverage requirement.

For timetabling, use a shared-room overlap as a negative fixture: two required
classes in the same room/time cannot pass merely because each was assigned.
For job/project scheduling, include a precedence boundary and an overlapping
resource-use case. State the expected verdict and run the target's evaluator
once the canonical model is available.

## Repair and interpretation

An unavailable employee needs baseline-aware repair; preference improvement on
a valid roster is re-optimization. Retain frozen/completed commitments, verify
that their new facts remain legal, and explain actual changes. Distinguish
count of violations from hours of shortage and feasible partial plans from
full coverage. Use [results and repair](../results-and-repair.md) and preserve
missing evidence rather than reconstructing a certificate from a table.
