# Embedded execution

## Establish the installed artifacts

Obtain the runtime, solver wheels and entitled license through
[published runtime access](https://helixor.dev/guide/quickstart.html), then
install the issued compatible artifact set in the application environment.
The [Preview tutorial](https://helixor.dev/tutorials/solver-deployment-models.html)
distinguishes `helixor-runtime[solvers]` (base routing) from
`helixor-runtime[solvers-full]` (rostering/HGS). These extras describe dependencies;
they do not make private artifacts available on a public package index.
The tested solver dependency requires Python 3.12 even though the Runtime
facade alone supports Python 3.11. Verify the whole artifact set's metadata.

Load the issued license with `HelixorSolver.load_license()`, which checks the
configured license file and normal runtime locations. A solve needs the
applicable solver entitlement. Pre-solve advice does not grant solve authority.
Never copy internal test signing helpers or substitute a development key.

## Minimal supplied problem

This small planar example uses coordinate units, not road-network kilometres.
Run it only after installing the artifact set and loading an entitled license.
The example intentionally states every required field; real customer
constraints still need the shared modeling and enforcement checks.

```python
from helixor_runtime import HelixorSolver

problem = {
    "coordinates": [[0, 0], [10, 0], [20, 0], [30, 0], [0, 10], [0, 20], [0, 30]],
    "demands": [0, 1, 1, 1, 1, 1, 1],
    "capacity": 3,
    "n_vehicles": 2,
    "distance_metric": "euclidean",
}
solver = HelixorSolver(mode="embedded", license=HelixorSolver.load_license())
validation = HelixorSolver.validate("vrp", problem)
assert validation["ok"], validation
preflight = solver.feasibility("vrp", problem)
assert preflight["verdict"] == "no_blocker_found", preflight
answer = solver.solve("vrp", problem,
                      options={"engine": "local_search", "time_limit_seconds": 0.3})
assert answer["verdict"] == "feasible", answer["shortfalls"]
assert answer["solution"] is not None
print(answer["metadata"]["model"], answer["cost"])
```

The checked example returns `embedded` and cost `120.0` coordinate units.
That result is about this supplied instance, not a quality or latency guarantee.
Inspect the complete [answer contract](contracts.md#read-the-answer) in an
application; the assertions here are smoke checks, not a substitute verifier.

For a deliberate capacity shortfall, keep the same problem and set
`n_vehicles` to `1`. The stated demand is six and fleet capacity is three:
`verdict` is `infeasible`, `solution` is `None`, and shortfalls/alternates explain
what must change. Do not promote an alternate to the user's accepted model.
