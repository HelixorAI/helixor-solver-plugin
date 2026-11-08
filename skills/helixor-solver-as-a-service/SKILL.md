---
name: helixor-solver-as-a-service
description: "Use for Helixor Solver service tasks: model or adapt an optimization problem, repair a plan, interpret a solve, discover capabilities, or integrate a hosted/customer-operated service with or without MCP. Includes routing, scheduling, allocation and container packing. Use solver-runtime for in-process embedding; generic OR questions alone do not imply Helixor use."
---

# Solver as a Service

Help the user turn a planning goal into a faithful model and an explained result.
This skill provides workflow guidance; it does not install/connect a service or
certify a deployment. Operational examples require the target's released
contracts and actual evidence. Apply the [source rules](../../sources.md).

Use the [shared solver navigator](../../solver/README.md) for the same modeling,
terminology, patterns and evidence guidance used by Solver Runtime. Execution
support still depends on the selected release, engine and interface.

1. Reuse the user's brief, data and existing model/plan. Select a recognized
   pattern with adaptation, custom definition, repair, result explanation or
   integration. Read only the relevant sections of [workflow](../../solver/workflow.md).
2. For new/adapted models, load [conversational intake](../../solver/modeling.md#conversation-before-implementation).
   Ask unresolved model-changing questions and wait for required answers; show
   the plain-language model, then author and validate its canonical manifest
   before integration code. Reuse complete models and known answers.
3. Once the brief is understood, proactively [offer a management/monitoring UX](../../solver/manifest-ui.md#offer-an-optional-management-ux),
   unless that choice is already known. An unanswered offer does not authorize
   UI creation or block supported non-UI work.
4. Before execution, verify the specific release, interface, admitted model,
   identity and allowed operation. Use the target's preparation/validation and
   result contracts. Unenforced required rules block the dependent solve and
   full-problem feasibility claims. Keep modeling without a live connection.
5. For repair, identify the baseline, changed facts and enforceable fixed/mutable
   scope. Use the supported repair contract; never silently substitute a fresh
   solve, weaken a hard rule or fabricate a baseline.
6. Report the actual plan, evidence, unmet demand, tradeoffs and next action.
   Missing proof stays missing. Separate solving from publication, dispatch,
   model activation and other downstream changes.

Load [terminology](../../solver/terminology.md) for unfamiliar names or OR layers,
[patterns](../../solver/patterns.md) for recipes, and
[modeling](../../solver/modeling.md) for adaptation/custom definition.
For prose-to-contract translation, read [LLM formulation](../../solver/formulation.md):
preserve symbolic relationships, bindings, source coverage and execution limits.
For service setup use [the service workflow](references/workflow.md) and
[integrations](references/integrations.md). For embedded execution or the
`HelixorSolver` facade, use Solver Runtime if present in
[the catalog](../../catalog.json); otherwise identify the missing runtime guide.
