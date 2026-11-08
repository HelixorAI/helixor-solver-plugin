# Terminology

These definitions describe the skill system. Service names below are routing
labels from the initial brief; service owners must verify their public meaning.

| Term | Meaning in this guidance |
| --- | --- |
| Skill | Instructions that help an AI select and follow a product workflow |
| Reference | Detail loaded by a skill when the current task needs it |
| Workflow | A documented sequence with inputs, prerequisites, outcomes, and failure paths |
| MCP connection | An AI-to-server tool interface; its presence and actual tool set must be verified |
| Embedded integration | Use of a supported runtime/library inside the customer's application or system |
| Hosted service | A service operated for the user; provider, environment, and contract need evidence |
| Self-hosted service | A service the customer operates; MCP exposure is a separate capability |
| Generated SDK | A client produced from the owning API contract, using its supported generation/distribution path |
| Draft guide | Planned guidance with unresolved product evidence; not an executable procedure |

Keep these distinctions explicit:

- A decision runtime and decision as a service are separate routing areas.
  Verify their respective contracts and relationship before mapping an API.
- A solver runtime and solver as a service are separate routing areas.
  A problem capability does not establish a hosting or access option.
- A digital worker workflow and a solver/decision invocation are not synonyms.
  Establish the owning lifecycle and authority boundary from source.
- MCP access, hosting, and embedded integration describe different choices.
  A user may need guidance without any tool connection.
- A candidate or recommendation is not execution truth. Preserve the owning
  contract's validation, admission, verification, and result evidence.

Use the name **Helixor Auto** as supplied; do not invent aliases or infer
behavior from its name. Label API fields
with a plain-language explanation only after verifying their exact meaning.
