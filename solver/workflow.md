# Choose the shared solver workflow

The [published Solver overview](https://helixor.ai/solver/) describes declarative
business-rule models and plan/certificate output. It is product context, not a
release-specific schema or deployment receipt. This guidance does not promise
that every recipe, formulation, repair control or interface is installed.

## Start at the needed depth

For new/adapted models, first follow [conversational intake](modeling.md#conversation-before-implementation):
resolve missing constraints/objectives, show the model, author/validate the
canonical manifest, then implement its integration. Both service and embedded
placement use this sequence. Once the brief is understood, proactively
[offer the optional management UX](manifest-ui.md#offer-an-optional-management-ux).
Reuse an existing choice and keep an unanswered offer independent of non-UI work.

| User need | Read next | Deliver |
| --- | --- | --- |
| Familiar problem with customer rules | [Patterns](patterns.md), then [Path A](modeling.md#path-a-adapt-a-known-pattern) | Starting structure, mapped facts, candidate model delta and checks |
| LLM translates prose or mathematical relationships | [Formulation](formulation.md) | Source-grounded variables, constraints, goal, coverage and precise gaps within the actual contract |
| Novel/hybrid problem or no single recipe fits | [Path B](modeling.md#path-b-define-a-custom-problem) | Decision brief, canonical candidate model/data contract, rule mapping, verification examples and gaps |
| Existing plan disrupted or needs improvement | [Results and repair](results-and-repair.md#repair-an-existing-plan) | Baseline, supported operation, protected commitments, changes and verified outcome |
| Prepare/validate data or execute a model | [Inputs and execution](inputs-and-execution.md) | Validated input/reference, bounded authorized call and actual result/state |
| Explain scores, partial output, failure or proof | [Results and repair](results-and-repair.md) | Actual verdict, coverage, evidence limits and concrete next action |
| Integrate a runtime or connect/operate a service | [Execution boundary](README.md#execution-boundary) and [shared mode selection](../workflows.md) | Owning guide, verified path, prerequisites, version/interface evidence and dependent gaps |
| Explain/preserve manifest UI, forms or views | [Manifest UI](manifest-ui.md) | Declaration-to-consumer trace, supported bindings and observed behavior/gaps |
| Reuse a model, export a plan, provide feedback | [Lifecycle and feedback](lifecycle-and-feedback.md) | Supported versioned lifecycle/output action within authority |

Move between paths without repeating answered intake. A supplied manifest or
existing model takes precedence over restarting from a demo. Pattern names
are hints about structure, not exact API identifiers. Read
[terminology](terminology.md) when meanings affect the model.

## Separate four evidence questions

1. What does the user mean? Establish decisions, facts, constraints and success.
2. Can the selected canonical contracts express that meaning? Map every material
   rule, validate the candidate artifact and check its behavior.
3. Can this deployment/interface execute it? Verify release, admission,
   discovered operations and authority. Schema validity alone is insufficient.
4. What did this run establish? Inspect returned plan, evaluated rules,
   certificate/status, provenance and missing evidence.

A missing preset can still lead to an expressible custom model. A demonstrated
missing primitive needs the owning shared extension; never omit the requirement
or write a substitute optimizer. Human-language interpretation proposes a
candidate; typed validation/admission and evaluation establish execution truth.

## Keep the answer useful

Lead with the chosen structure or observed outcome. Explain only the terms and
questions that affect the task. Preserve unknowns and identify the exact next
input or check. Do not burden a standard ready-to-model problem with the full
custom interview. No MCP is required to read, explain or define a problem.

For any operational example, retain source URL, release/schema/model version,
verification date, applicable mode and actual observed limits. Follow
[shared evidence rules](../sources.md). Do not infer endpoints, SDK
symbols, repair tools or automatic retries from a website example.
