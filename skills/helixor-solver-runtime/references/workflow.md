# Solver Runtime workflow

Use the [shared solver navigator](../../../solver/README.md) for modeling,
[terminology](../../../solver/terminology.md), [patterns](../../../solver/patterns.md),
result interpretation, repair and lifecycle questions. This workflow owns the
runtime's execution boundary and versioned invocation, not a second set of
solver definitions.

## Choose the execution boundary

| User task | Path |
| --- | --- |
| Solve inside the application with no network call | [Embedded](embedded.md), with installed solver and entitled license |
| Call a running local or remote solver service | [Hosted](hosted.md), with generated client, service address and its authorization |
| Deploy the service, publish a solver pack or configure MCP | Use the solver service skill if present in [the catalog](../../../catalog.json); otherwise state the missing service guidance. Qualify that interface separately |
| Explain a result, frame a model or inspect inputs without MCP | Continue with the supplied evidence; no connection is needed for reading or supported local checks |

Choose the mode from the user's architecture. `HelixorSolver` requires it
explicitly. In hosted mode the problem data crosses the service boundary;
verify the intended environment and authority before sending it. Neither mode
falls back to the other. A missing package, license, token or reachable service
is a specific prerequisite failure, not permission to invent another route.
The [published tutorial](https://helixor.dev/tutorials/solver-deployment-models.html)
labels both models Preview.

## Model before executing

Use the [shared intake](../../../solver/modeling.md#conversation-before-implementation)
for new/adapted problems: identify decisions, input units, mandatory rules,
preferences, objective and missing facts. Preserve requirement provenance.
Show the plain-language model, author/validate the applicable manifest, and
check enforcement before integration code. Do not repeat intake for a complete
existing model or an integration-only request.

The tested `HelixorSolver.solve` contract accepts `vrp` and `rostering`.
A wider server manifest catalog does not enlarge this facade automatically.
An unfamiliar shape needs an admitted manifest/extension and the owning
engine contract; do not squeeze it into VRP or add domain branches to core.

Keep three contracts distinct:

- Runtime `SolverManifest`: backend-neutral problem data, constraints,
  feasibility checks, objectives, adapters and metadata.
- Authoring/UI schema: richer authoring fields such as domain/version and UI
  surfaces. It is not the runtime dataclass.
- `SolveRequest`: the service/worker request boundary. The Runtime facade takes
  `problem_type`, a problem mapping and supported options, then uses the
  owning solve contract. Reasoner `SolveReport` is a separate contract.

Use the installed manifest loader/validator and declared extension packs.
Reusing an engine policy does not prove that an added business rule is enforced.

## Prepare, solve and explain

1. Inspect `HelixorSolver.describe_inputs(problem_type)` and
   `HelixorSolver.validate(problem_type, problem)` for the current input shape,
   missing fields and defaults. These static helpers run locally, including
   when you configured a hosted solver; they are not a probe of that server.
2. Use the configured solver's `recommendations(...,
   recommendation_type="constraints")` to inspect declared classes and
   enforcement, or `"data"` / `"parameters"` for those questions. Check which
   constraints are skipped, merely proposed or not enforced by the selected
   engine. Do not attribute a preset limit to the user.
3. Call `solver.feasibility(problem_type, problem)` for necessary pre-solve
   checks. `infeasible` names a blocker. `no_blocker_found` means only that no
   declared check failed; the solve and certificate must still establish a plan.
4. Call `solver.solve(..., options=...)` with the stated engine/budget. Inspect
   the [complete answer](contracts.md#read-the-answer), including enforcement
   limits, before reporting feasibility for the user's whole problem.
5. If infeasible, explain named shortfalls and ranked relaxed alternatives.
   An alternative states what it relaxes; it is not an accepted policy change
   or the original problem's solution. Ask for the material business decision
   before solving a changed problem.

After the brief, make the [optional UX offer](../../../solver/manifest-ui.md#offer-an-optional-management-ux).
Keep it independent of runtime invocation. Existing consumers/generated seams
own an accepted UI; do not create polling or a second solver implementation.

For workforce input, follow the [small rostering example](rostering.md) after
configuring the chosen mode.

## Verification scope

The [version record](contracts.md#versions-and-sources) describes the inspected
Preview contracts. The current local checks exercise embedded and real local
HTTP routing, roster feasibility, typed errors and independent route/roster
scoring. They do not qualify production identity, remote workers, GPU
execution, custom packs, every problem size, or every AI host. Confirm the
actual target rather than extrapolating from a local run.
