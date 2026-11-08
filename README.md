# Helixor Solver plugin for Cursor

This plugin teaches the Cursor agent how to work with Helixor Solver. It helps
you model an optimization problem (routing, scheduling, rostering, packing,
allocation) and integrate the Helixor solver runtime or a solver service. It
also explains solve results and failures.

The plugin is guidance only. It contains Markdown skills and no executable
code, hooks or MCP configuration. Installing it does not install the solver,
supply a licence or connect a service.

Status: **Preview**, version 0.1.0.

## What you get

| Skill | Use it for |
| --- | --- |
| `helixor-solver-runtime` | Calling `HelixorSolver` from `helixor_runtime`, embedded or hosted; routing and rostering inputs; feasibility checks; reading results and typed failures |
| `helixor-solver-as-a-service` | Working with a solver service: its contract, problem discovery, pack publication and result verification |
| `helixor-platform` | Choosing between the two when you have not picked one |

Both solver skills share the modeling guidance in [`solver/`](solver/README.md):
terminology, problem patterns, formulation, inputs, results and repair.

## Install

You need Cursor and `git` (or a ZIP tool). In an organization, an
administrator may need to allow local plugins.

The plugin installs into `~/.cursor/plugins/local/helixor-solver/`. That
folder must contain `plugin.json` and `skills/` directly, not in a nested
folder.

### From the repository

```bash
git clone --branch v0.1.0 https://github.com/HelixorAI/helixor-solver-plugin.git
```

```bash
mkdir -p ~/.cursor/plugins/local/helixor-solver
```

```bash
cp -R helixor-solver-plugin/. ~/.cursor/plugins/local/helixor-solver/
```

```bash
rm -rf ~/.cursor/plugins/local/helixor-solver/.git
```

### From the release ZIP

Download `helixor-solver-0.1.0-cursor.zip` and `SHA256SUMS` from the
[v0.1.0 release](https://github.com/HelixorAI/helixor-solver-plugin/releases/tag/v0.1.0)
into one folder. Check the ZIP, then extract it:

```bash
shasum -a 256 -c SHA256SUMS
```

```bash
mkdir -p ~/.cursor/plugins/local/helixor-solver
```

```bash
unzip helixor-solver-0.1.0-cursor.zip -d ~/.cursor/plugins/local/helixor-solver
```

The check prints `helixor-solver-0.1.0-cursor.zip: OK`. The ZIP holds the same
files as tag `v0.1.0`.

### Load it

- **Cursor app**: open the Command Palette and run **Developer: Reload
  Window**. Open **Customize** and check that the plugin and its skills are
  listed. Start a new Agent chat so the skills load.
- **Cursor agent CLI** (`cursor-agent`): no reload is needed. The next run
  picks up the plugin.

### Confirm the install

Ask the agent:

```text
List the installed Helixor solver skills and briefly explain when to use each one. Do not change files or connect services.
```

It names `helixor-platform`, `helixor-solver-as-a-service` and
`helixor-solver-runtime`, and describes each one. With the plugin folder
removed, the same question gets the answer that no Helixor solver skills are
installed.

## Run a solve

The agent writes integration code. To run that code, you need the Helixor
runtime and a solver service to call.

### Prerequisites

- Python 3.12.
- The Helixor runtime wheels you receive with your licence:
  `helixor_runtime-0.3.1-py3-none-any.whl`,
  `helixor_constraint_network-1.0.1-py3-none-any.whl` and `SHA256SUMS`. See
  [Installation](https://helixor.dev/guide/installation.html).
- The runtime's `solvers-hosted` extra. It installs the hosted solver client,
  `helixor-solver-contract`, from a Git repository, so your Helixor contact must
  give you access to that repository first.
- A solver service address and a token for it.

Install into a virtual environment, from the folder that holds the wheels:

```bash
python3.12 -m venv .venv
```

```bash
shasum -a 256 -c SHA256SUMS
```

```bash
.venv/bin/python -m pip install "./helixor_runtime-0.3.1-py3-none-any.whl[solvers-hosted]" ./helixor_constraint_network-1.0.1-py3-none-any.whl
```

### Point the client at a service

The client reads two environment variables. It sends the token as
`Authorization: Bearer <token>` and sends no other identity headers.

```bash
export HELIXOR_SOLVER_URL=<your solver service address>
```

```bash
export HELIXOR_SOLVER_TOKEN=<your token>
```

If you run `helixor-solver-server` yourself for local testing, start it on any
free port with authentication off and local pack storage:

```bash
HELIXOR_AUTH_DISABLED=1 HELIXOR_SOLVER_PACK_STORAGE=local python -m uvicorn helixor_solver_server.app:app --host 127.0.0.1 --port 8463
```

Then set `HELIXOR_SOLVER_URL=http://127.0.0.1:8463`. With authentication off,
any token value works. The example script still reads
`HELIXOR_SOLVER_TOKEN`, so set it to any non-empty value.

### Worked example: two vans, six stops

Ask the agent:

```text
Use the Helixor solver runtime in hosted mode. Write solve_routes.py. The script reads the service address from HELIXOR_SOLVER_URL and the bearer token from HELIXOR_SOLVER_TOKEN. It plans delivery routes: one depot at (0,0), six customers at (10,0), (20,0), (30,0), (0,10), (0,20), (0,30), each with demand 1, two vans of capacity 3, euclidean distance. It prints the verdict, cost and routes, and the shortfalls if the answer is not feasible. Send no realm or tenant headers.
```

The agent wrote this script:

```python
import os
from helixor_runtime import HelixorSolver

problem = {
    "coordinates": [[0, 0], [10, 0], [20, 0], [30, 0], [0, 10], [0, 20], [0, 30]],
    "demands": [0, 1, 1, 1, 1, 1, 1],
    "capacity": 3,
    "n_vehicles": 2,
    "distance_metric": "euclidean",
}

solver = HelixorSolver(
    mode="hosted",
    base_url=os.environ["HELIXOR_SOLVER_URL"],
    auth=os.environ["HELIXOR_SOLVER_TOKEN"],
    timeout_seconds=30,
)

answer = solver.solve(
    "vrp",
    problem,
    options={"engine": "local_search", "time_limit_seconds": 0.3},
)

print(answer["verdict"], answer["cost"], answer["solution"])
if answer["verdict"] != "feasible":
    print(answer["shortfalls"])
```

Run it with the virtual environment's Python:

```bash
.venv/bin/python solve_routes.py
```

The client sends `POST /api/v1/solve/vrp` to the service. The answer:

```text
feasible 120.0 {'routes': [[0, 3, 2, 1, 0], [0, 6, 5, 4, 0]], 'route_rows': [{'vehicle': 1, 'stops': [0, 3, 2, 1, 0], 'load': 3.0, 'distance': 60.0}, {'vehicle': 2, 'stops': [0, 6, 5, 4, 0], 'load': 3.0, 'distance': 60.0}], 'distance': 120.0, 'distance_unit': 'coordinate_units', 'distance_metric': 'euclidean'}
```

Each van serves one line of three stops and travels 60 coordinate units, for a
total cost of 120. Distances are in coordinate units, not kilometres.

To see a failure, change `"n_vehicles": 2` to `"n_vehicles": 1` and run it
again. The verdict is `infeasible`, the cost and solution are `None`, and the
shortfall names the cause:

```text
infeasible None None
[{'kind': 'pre_solve_check', 'check_id': 'fleet_capacity', ..., 'demand': 6.0, 'supply': 3.0, 'deficit': 3.0, ..., 'message': 'Total demand is 6 units but the fleet carries 3 (1 vehicle(s) x 3); shortfall 3 units. No route plan can serve every stop. Review: Fleet -> Vehicle count and capacity.', ...}]
```

If the service cannot be reached or answers outside the solve contract, the
client raises `SolverServiceError`. It does not fall back to solving locally.

## Update and remove

To update, replace the contents of `~/.cursor/plugins/local/helixor-solver/`
with the new version and reload the Cursor window. To remove the plugin,
delete that folder and reload.

## Troubleshooting

| Symptom | Check |
| --- | --- |
| Local plugins are blocked | Your organization controls plugin imports. Ask your administrator to allow this plugin. |
| The folder is present but no skills load | Look for an extra folder level. The destination must contain `plugin.json` and `skills/` directly. Reload after fixing it. |
| `pip` cannot fetch `helixor-solver-contract` | The `solvers-hosted` extra needs access to its Git repository. Ask your Helixor contact for access. |
| `KeyError: 'HELIXOR_SOLVER_URL'` | Export both environment variables in the shell that runs the script. |
| `SolverServiceError` | Check the service address, that the service is running, and the token. |

## Licence

Copyright © 2026 Helixor AI, Inc. All rights reserved. See [LICENSE](LICENSE).
The Helixor runtime and services are licensed separately.
