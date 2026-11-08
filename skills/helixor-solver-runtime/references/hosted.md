# Calling a local or remote service

Hosted means the Runtime calls a service, even when that service is on this
machine. Install the generated `helixor-solver-contract` client from the
approved artifact set (`helixor-runtime[solvers-hosted]` dependency route).
Use the actual service address and token; the client has no default host.
The [published Preview tutorial](https://helixor.dev/tutorials/solver-deployment-models.html)
uses the same facade and result contract in both modes.

After establishing a supported service and the authorization to send the data,
configure the following instead of the embedded constructor. `problem` is the
explicit small input from the [embedded example](embedded.md).

```python
import os
from helixor_runtime import HelixorSolver

solver = HelixorSolver(mode="hosted",
                      base_url=os.environ["HELIXOR_SOLVER_URL"],
                      auth=os.environ["HELIXOR_SOLVER_TOKEN"],
                      timeout_seconds=30)
answer = solver.solve("vrp", problem,
                      options={"engine": "local_search", "time_limit_seconds": 0.3})
assert answer["metadata"]["model"] == "hosted"
assert answer["verdict"] == "feasible", answer["shortfalls"]
print(answer["metadata"]["model"], answer["cost"])
```

The supplied example returns `hosted` and cost `120.0` coordinate units.
A different instance or stochastic engine can produce a different cost; compare
verdicts, evidence, engines and a declared tolerance rather than identical bytes.
A timeout/unreachable service is `SolverServiceError`, not permission to run a
local engine. Missing/invalid data and unsupported options keep their typed
[contract failures](contracts.md#typed-failures).

A service operator can run the supplied server distribution locally with its
supported configuration, using `python -m uvicorn helixor_solver_server.app:app
--host 127.0.0.1 --port <chosen-port>`. Check port ownership first, retain its
startup result, and terminate only the process started for the test. A local
process still needs its declared dependencies and configured authorization.
An embedded license is not a service token. Do not disable identity checks to
make a customer integration work; isolated producer test fixtures do not
establish production identity support.

No MCP is involved in this client path. For deployment, pack publication,
worker/GPU topology or MCP exposure, use the
service skill when present in [the catalog](../../../catalog.json) and establish those
interfaces separately. Do not equate `HelixorSolver.solve`'s two tested problem
types with every problem advertised by a server manifest catalog.
