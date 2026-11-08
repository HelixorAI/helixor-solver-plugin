# Helixor Solver plugin for Cursor

This plugin teaches the Cursor agent how to work with Helixor Solver. It helps
you model an optimization problem (routing, scheduling, rostering, packing,
allocation) and integrate the Helixor solver runtime or the hosted solver
service. It also explains solve results and failures.

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

## Requirements

- Cursor with plugin support. In an organization, an administrator may need to
  allow local or repository plugins.
- To run solves, you also need Helixor solver access:
  - **Embedded**: the Helixor runtime and solver packages, plus an entitled
    licence. See the [quickstart](https://helixor.dev/guide/quickstart.html).
  - **Hosted**: a solver service address and an access token.

  The [deployment models tutorial](https://helixor.dev/tutorials/solver-deployment-models.html)
  explains both modes.

## Install

### Option A: from this repository URL

1. In Cursor, open **Customize** and go to the plugin search.
2. Paste this repository's URL:

   ```text
   https://github.com/HelixorAI/helixor-solver-plugin
   ```

3. Select **Install**, then choose user or project scope.

### Option B: from a local copy

Use this route when you want to pin an exact version, or when repository
plugins are not available to you.

```bash
git clone https://github.com/HelixorAI/helixor-solver-plugin.git
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

`plugin.json` must sit directly in `~/.cursor/plugins/local/helixor-solver/`,
not in a nested folder.

To pin a release, check out its tag after cloning, for example
`git -C helixor-solver-plugin checkout v0.1.0`.

Each [release](https://github.com/HelixorAI/helixor-solver-plugin/releases)
also has a ZIP of the same files and a `SHA256SUMS` file. To use the ZIP, check
its hash, extract it into the same folder, and continue with the reload step:

```bash
shasum -a 256 -c SHA256SUMS
```

### Reload and confirm

1. Open the Command Palette and run **Developer: Reload Window**.
2. Open **Customize** and find **helixor-solver**. Its skills should be listed
   with no manifest or missing-file errors.
3. Start a new Agent chat so the skills load.

A safe first prompt:

```text
List the installed Helixor solver skills and briefly explain when to use each one. Do not change files or connect services.
```

## Use

Describe your problem in plain terms, attach or point to your data, and say
whether you want embedded or hosted execution. The agent asks about anything
that changes the model before it writes integration code.

Example prompts:

```text
I need to plan delivery routes for 12 vans from one depot, with customer time windows and van capacity. Help me model it for the Helixor solver before writing any code.
```

```text
Using the Helixor runtime in embedded mode, write a small script that solves this routing problem and prints the verdict, cost and any shortfalls.
```

```text
My hosted solve came back infeasible. Here is the response. Explain what blocked it and what I could change.
```

What to expect:

- The agent separates the rules you gave from defaults and assumptions.
- The agent picks embedded or hosted mode only on your instruction. It never
  falls back from one mode to the other on its own.
- An infeasible result is reported as infeasible, with the reasons. The agent
  does not relax your rules to make a plan look feasible.

## Update and remove

- **Option A**: update or uninstall from Cursor's plugin panel.
- **Option B**: replace the contents of
  `~/.cursor/plugins/local/helixor-solver/` with the new version, then reload
  the window. To remove the plugin, delete that folder and reload.

## Troubleshooting

| Symptom | Check |
| --- | --- |
| Local plugins are blocked | Your organization controls plugin imports. Ask your administrator to allow this plugin. |
| The folder is present but no skills load | Look for an extra folder level. The destination must contain `plugin.json` and `skills/` directly. Reload after fixing it. |
| Two copies appear | A repository install and a local copy can both be present. Keep one. |
| Skills load but a solve fails to start | The plugin does not supply the runtime, a licence or a service token. Set those up from the requirements above. |

## Licence

Copyright © 2026 Helixor AI, Inc. All rights reserved. See [LICENSE](LICENSE).
Helixor runtime and services are licensed separately.
