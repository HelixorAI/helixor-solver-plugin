# Shared solver guidance

Use this guidance for both Solver Runtime and Solver as a Service. Execution
placement changes setup and invocation, while the problem's meaning, required
rules and evidence obligations remain the same. Read only the sections needed
for the user's task.

| Need | Read |
| --- | --- |
| Choose a modeling, repair or explanation path | [Workflow](workflow.md) |
| Understand problem families, formulations, methods, evidence or uncertainty | [Optimization terminology](terminology.md) |
| Choose a starting structure | [All pattern recipes](patterns.md): routing/scheduling, scheduling/timetabling, packing/consolidation, allocation/inventory |
| Translate prose or math into a source-grounded solver candidate | [LLM formulation](formulation.md) |
| Structure a VRP brief for generation and validation | [VRP formulation](vrp-formulation.md) |
| Structure container allocation or physical loading requirements | [Container formulation](container-formulation.md) |
| Clarify requirements, adapt a pattern or define a custom problem | [Modeling and provenance](modeling.md) |
| Prepare data, check enforcement or execute within a verified contract | [Inputs and execution](inputs-and-execution.md) |
| Interpret a plan, failure, proof or baseline-aware repair | [Results and repair](results-and-repair.md) |
| Offer or preserve a model's optional management UX | [Manifest UI](manifest-ui.md) |
| Reuse/version a model, present outputs or handle feedback | [Lifecycle and feedback](lifecycle-and-feedback.md) |

## Execution boundary

Use [the catalog](../catalog.json) to find the installed guide for the selected
boundary. Solver Runtime owns `HelixorSolver` embedded/hosted invocation and its
versioned contracts. Solver as a Service owns service deployment/operation,
MCP setup and pack publication guidance. For a missing guide, identify that
documentation gap; continue supported modeling and explanation.

Choose placement using [shared mode selection](../workflows.md), then follow
the owning guide's release-specific setup and invocation. This shared material
requires no MCP connection for reading or modeling. A term, recipe, manifest or
valid model does not establish that an installed facade, engine or deployment
can execute it. Verify that exact target's input, enforcement, result and
authority contracts. Apply the [source rules](../sources.md).
