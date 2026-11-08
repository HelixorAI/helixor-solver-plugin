---
name: helixor-solver-runtime
description: "Use for HelixorSolver embedded or hosted runtime integration, routing and rostering inputs, feasibility checks, solve results and typed failures. Use solver-as-a-service for service deployment, pack publication or MCP setup; a generic optimization question alone does not imply Helixor."
---

# Solver Runtime

Use `HelixorSolver` from `helixor_runtime` to run an explicitly selected
embedded or hosted solve. This interface is **Preview**. Verify the installed
artifacts and deployment against the [version and source record](references/contracts.md#versions-and-sources);
installing this skill supplies neither the engine nor a license or connection.

Use the [shared solver navigator](../../solver/README.md) for modeling and
explanation. Load [terminology](../../solver/terminology.md) when names or OR
layers matter, [patterns](../../solver/patterns.md) for a starting structure,
and the [shared workflow](../../solver/workflow.md) for data, results, repair
and lifecycle questions. These references do not expand the installed runtime's
supported problem types or operations.

For LLM-generated problem candidates, read [formulation](../../solver/formulation.md)
for symbolic relationships, bindings and source coverage. This does not expand
the Preview facade's supported mathematical or optimization contracts.

1. Start with the user's brief, data and existing model. For a new/adapted
   problem, use the [shared modeling conversation](../../solver/modeling.md#conversation-before-implementation)
   before integration code. Reuse answered questions and complete models;
   [attribute supplied requirements](../../solver/modeling.md#attribute-facts-and-constraints)
   separately from defaults, possible constraints and engine limitations.
2. Use [the workflow](references/workflow.md) to choose embedded or hosted.
   There is no default and no automatic fallback between them. A local HTTP
   server is hosted mode; embedded means execution inside this process.
3. Establish artifacts, version, license or token and input contract. Follow
   [embedded setup and example](references/embedded.md) or
   [hosted setup and example](references/hosted.md). Reading and embedded
   modeling do not require MCP.
4. Validate supplied data and inspect declared constraint enforcement. A
   preflight with no blocker is not a feasible plan. Required rules that lack
   enforcement block the dependent solve and a full-feasibility claim.
5. Interpret [the solve contract and typed failures](references/contracts.md).
   Keep the actual model, engine, certificate, shortfalls and alternatives;
   an infeasible answer has no usable solution. Never relax a user rule or
   switch modes to turn a failure into a success.
6. Once the brief is understood, [offer an optional management/monitoring UX](../../solver/manifest-ui.md#offer-an-optional-management-ux)
   unless the choice is known. An unanswered offer authorizes no UI work and
   does not block supported non-UI work.

Return the checked plan or precise failure, its evidence and limits, and the
next supported action. Solving does not authorize dispatch, publication,
rule activation or other downstream effects. Use existing manifests, engines
and generated SDKs; do not build a substitute optimizer or client.
