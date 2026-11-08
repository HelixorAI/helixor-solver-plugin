# Runtime contracts and failures

## Versions and sources

Checked 2026-11-03 against the published
[embedded/hosted solver tutorial](https://helixor.dev/tutorials/solver-deployment-models.html),
[Python reference](https://helixor.dev/reference/python.html) and
[runtime access/quickstart](https://helixor.dev/guide/quickstart.html).
The solver tutorial is Preview and requires Runtime 0.3.0 or later and the
separate 0.7 solver artifact for embedding.

The local verification used these installed distributions from exact artifacts:

| Distribution | Version / purpose |
| --- | --- |
| `helixor-runtime` | 0.3.1; public `HelixorSolver` facade |
| `helixor-solvers` | 0.7.1; solve contract version `1`, engines and manifests |
| `helixor-solver-contract` | 0.1.0; generated hosted client, release `helixor-solver-contract-sdk/v0.1.0` |
| `helixor-solver-server` | 0.2.0; actual local HTTP producer |
| `helixor-core` | 1.1.0; released shared dependency |
| `helixor-reasoning` | 1.0.0; released dependency compatible with that Core |

These are a verification snapshot, not an instruction to upgrade a customer's
installation or a promise about every compatible version. Use the issued
artifact set and the deployment's contract. Keep Core and Reasoning from the tested released artifact set together; an
unpublished development snapshot may require extension contracts absent from
a released Core. The runtime wheel excludes the
solver engine and internal license-authority test helpers. Do not suggest
unavailable registry packages or instruct a customer to mint their own license.
A lower-version solver without `solve_contract` cannot serve this facade.

## Read the answer

`solver.solve("vrp" | "rostering", problem, options=...)` returns a mapping:

| Field | Interpretation |
| --- | --- |
| `contract_version` | Contract identity; checked version is `1` |
| `verdict` | `feasible` or `infeasible` for what the certificate checked |
| `solution` | Usable routes/roster only for a feasible verdict; otherwise `None` |
| `shortfalls` | Named failed checks, unmet demand or violated rules |
| `alternates` | Ranked options describing the rules/parameters they relax |
| `certificate` | Feasibility evidence and the rejected plan when present |
| `metadata` | Actual `model`, engine and reason, budget, seed/final cost and limits |
| `cost` | Objective value with the reported unit; do not invent a cost when absent |

Do not claim global optimality from a feasible certificate or a time budget.
Keep `certificate` enforcement limits and skipped checks visible. A candidate
that satisfies some rules does not establish the user's whole model. In
particular, time windows, driver-hours limits and return deadlines are distinct
requirements; inspect the selected engine's enforcement for each one.

## Engines and inputs

For routing, `options.engine` is `auto`, `local_search` or `hgs`. `auto` selects
local search for time windows; otherwise HGS if its dependencies are available,
else local search, with the reason reported. Explicit `hgs` with time windows
is refused; a missing requested engine is an error. The base routing path is
pure Python; HGS and rostering require the full dependency set. Use the
producer's options for roster engine selection rather than copying VRP options.

The minimal example uses aligned `coordinates` (depot first), `demands`,
`capacity`, `n_vehicles` and an explicit `distance_metric`. Customer records
with time windows additionally need declared travel speed, depot horizon,
service-time units and applicable vehicle limits. Do not invent them. Read the
input description/validation result before importing customer data.

## Typed failures

| Runtime error | Meaning / next action |
| --- | --- |
| `SolverConfigurationError` | Missing/unknown mode or contradictory configuration; fix the declared boundary |
| `SolverInputError` | Invalid/missing problem inputs; retain `failure_code` and missing-field detail, correct the stated data |
| `SolverOptionError` | Unsupported option or problem type; preserve the refusal and use a supported contract |
| `SolverEngineUnavailableError` | Required engine/dependency unavailable; install the admitted artifact or explicitly choose another supported engine |
| `SolverServiceError` | Hosted connection failure or response outside the contract; inspect the target/response, do not switch to embedded |
| `SolverLicenseRequiredError` and other license errors | Embedded entitlement is absent, invalid, expired or insufficient; use the issued license and its permitted capabilities |

Input/option faults map to HTTP 422 and unavailable engines to 503 in the
service contract. The generated client preserves their Runtime error classes.
Transport failures are separate from an infeasible result. Do not catch an
exception and return an empty plan or fabricated success.
