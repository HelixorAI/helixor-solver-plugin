# Solver service workflow

Start with the [shared solver navigator](../../../solver/README.md) and
[task workflow](../../../solver/workflow.md) for modeling, patterns, data,
results, repair, optional UX and lifecycle guidance. Runtime and service users
use the same definitions and modeling obligations.

For service deployment/operation, MCP setup or pack publication, follow
[service integrations](integrations.md) and verify the target's released
contracts and authority. Pack lifecycle distinctions are in the
[shared lifecycle guide](../../../solver/lifecycle-and-feedback.md); a solve
never authorizes publication or activation.

For in-process integration or the `HelixorSolver` facade, use Solver Runtime
if present in [the catalog](../../../catalog.json). If absent, report the
missing guide without inventing a runtime setup. Shared vocabulary and recipes
do not expand the chosen execution contract.
