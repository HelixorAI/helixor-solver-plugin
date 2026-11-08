# Optimization vocabulary

Names suggest structure; actual decisions and constraints determine the model.
Preserve the user's term and explain a contextual synonym, narrower variant or
overlap where useful. Human names are separate from exact producer identifiers.
No table here is a list of installed Helixor capabilities.

## Problem families and structural patterns

| Term | Decision and important distinction |
| --- | --- |
| Assignment / matching | Associate items with resources or compatible pairs; establish cardinality, eligibility and whether unmatched items are allowed |
| Generalized Assignment Problem (GAP) | Assign jobs with agent-dependent costs/resource use under capacities; GAP is not an optimality gap |
| Knapsack | Select valuable items under resource limits; not necessarily place all demand |
| Bin packing / cutting stock | Place required items using bins or cutting patterns; typically reduce container/stock use or waste. State geometry and admissible cuts |
| Set covering / packing / partitioning | Select subsets for at-least-once / at-most-once / exactly-once participation. Set packing is not geometric packing |
| Shortest path / maximum flow / minimum-cost flow | Optimize paths or network quantities/costs under supplies, demands and capacities; not automatically vehicle tours or indivisible jobs |
| Transportation / transshipment | Allocate supply to demand directly or through intermediate nodes; flow is not necessarily a vehicle route |
| Facility location / location–allocation | Choose facilities and demand assignments; fixed facilities with only assignment decisions have narrower scope |
| Job shop / RCPSP | Ordered job operations on machines / Resource-Constrained Project Scheduling with precedence and limited resources. Neither is automatically employee rostering |
| TSP / CVRP / MDVRP | Traveling Salesperson Problem / Capacitated Vehicle Routing Problem / Multi-Depot VRP; confirm fleet, depot and visit assumptions |
| Pickup-and-delivery | Paired tasks with precedence and load semantics, not unrelated visits |
| Lot sizing / replenishment | Quantities and timing with inventory balance; distinct from predicting demand |
| IRP / PRP | Inventory Routing Problem / Production Routing Problem: coupled replenishment/routing, with production decisions in PRP |

Precedence is a relation; makespan is schedule completion span; tardiness is
positive lateness beyond a due date. They are not separate solution algorithms.
See the [recipe index](patterns.md) for worked structures.

## Formulations and paradigms

| Term | Meaning |
| --- | --- |
| LP | Linear programming: continuous variables, linear objective/constraints |
| IP / ILP | Integer programming / integer linear programming; confirm integrality and expression class |
| MIP / MILP | Mixed-integer programming / mixed-integer linear programming; discrete decisions, possibly continuous ones; MILP specifies linearity |
| QP / MIQP | Quadratic objective with linear constraints / integrality added. Identify quadratic constraints separately |
| NLP / MINLP | Nonlinear programming / mixed-integer nonlinear programming. Confirm convexity and local/global scope |
| CP / CSP / constraint optimization | Constraint programming paradigm / feasibility-only Constraint Satisfaction Problem / constraint model with an objective |

CP can also mean critical path. Clarify context. Do not invent a business
objective for a satisfaction-only task. A user mentioning MILP may mean a
formulation, backend requirement or discrete decision model. CP-SAT is a solver
technology, not a business family or evidence it is available here.

## Methods

| Term | Role and limit |
| --- | --- |
| Exact search, branch-and-bound, cutting planes | Search/proof approaches; a time limit can stop before proof |
| Heuristic, metaheuristic, local search | Generate/improve candidates; tabu, simulated annealing and evolutionary search do not make a candidate optimal by name |
| Column generation | Restricted master plus pricing of useful columns; relaxation optimality is not automatically integer optimality |
| Benders decomposition | Master/subproblem information and cuts; preserve coupling rather than assume splitting proves correctness |
| Constraint propagation | Reduce variable domains; domain reduction alone is not a complete plan or optimality proof |

A family can have several formulations and methods. Select only an available,
applicable execution contract; describe the actual engine from run metadata.

## Evidence

| Term | Interpretation |
| --- | --- |
| Incumbent | Best currently known feasible candidate under the run's ranking; not necessarily globally optimal |
| Primal/dual or objective bound | For minimization, a feasible objective gives an upper bound and an applicable dual bound a lower bound; reverse for maximization. A heuristic score is not automatically a bound |
| Absolute/relative optimality gap | Separation from a valid bound under producer normalization. Keep units, denominator/zero behavior; no bound means gap unavailable |
| Feasible / infeasible / unbounded / unresolved | Candidate satisfies modeled rules / proof of no admissible solution / objective has no finite bound / result not established. No candidate in budget or execution failure proves neither infeasibility nor unboundedness |
| Tolerance / slack | Numerical acceptance criteria / margin to a rule boundary under a stated convention. Neither authorizes changing a business requirement |
| Shadow price, dual value, sensitivity | Model-dependent marginal information, often for a continuous model or relaxation; not arbitrary finite-change or integer/causal guarantees |
| IIS / conflict / unsatisfiable core | Irreducible Inconsistent Subsystem is minimal under deletion, not necessarily minimum size. Other conflict/core guarantees differ; generic violations are not automatically an IIS |

A feasibility certificate is not automatically a bound, gap, sensitivity report
or IIS. Return evidence as unavailable when absent.

## Uncertainty and planning

Distinguish deterministic fixed inputs from stochastic models of uncertain
outcomes; randomized search on fixed data is not stochastic optimization.
Scenarios are cases, not automatically calibrated probabilities. Recourse and
two-/multi-stage models specify what decisions can adapt after which information,
including non-anticipativity. Robust optimization needs an uncertainty set and
criterion; chance constraints need a probability model and requirement.
A historical quantile alone is not a joint probability guarantee.
Rolling horizons advance planning while carrying commitments; the phrase does
not authorize unattended scheduling, polling or production changes.

## Names within routing and loading

VRSP broadly describes routing plus scheduling; VRPTW adds visit time windows.
Field service, technician dispatch/TRSP and workforce routing may additionally
require qualifications, teams and duties. IPDS (Integrated Production and
Distribution Scheduling) includes production decisions coupled with delivery;
fixed goods-ready times alone do not make production a decision. These labels
overlap without being universal aliases. Clarify only unknown material facts:
arrival/start/finish windows, waiting, hard/soft bounds, duties, skills and fixed
readiness versus joint production. See [routing](patterns/routing-and-scheduling.md).

Container consolidation assigns cargo to load units; 2D/3D loading places it
spatially. CLP/CPP means container loading/packing problem in context;
palletization can add stacking/layers. Multiple resource capacities are not
spatial coordinates. Single-container value selection differs from shipping all
items with enough containers. See [containers](patterns/packing-and-consolidation.md).

## Definition sources

These primary references explain general terms; they do not establish Helixor
support. Checked 2026-10-30; use their definitions, not tool capability claims.

- [Set-constraint definitions](https://www.scipopt.org/doc/html/cons__setppc_8h_source.php),
  [solution methods](https://scipopt.org/doc/html/APPLICATIONS.php),
  [project-scheduling research](https://www.projectmanagement.ugent.be/research).
- [Robust modeling](https://pyomo.readthedocs.io/en/stable/explanation/solvers/pyros/index.html).

- [Technician-routing terminology](https://arxiv.org/abs/2211.16968),
  [integrated production/distribution scheduling](https://eprints.soton.ac.uk/426655/),
  [production-routing terminology](https://doi.org/10.1016/j.cor.2014.01.011),
  [generalized assignment](https://leeds-faculty.colorado.edu/glover/TS%20-%20vignettes%20-%20GAP%20Yagiura%20%26%20Ibaraki.pdf),
  and [container loading with stability/load-bearing](https://www.sciencedirect.com/science/article/pii/S0305054810001486).
  These support names and structural distinctions; abstract-only evidence does
  not establish implementation, benchmark results or operational guarantees.
