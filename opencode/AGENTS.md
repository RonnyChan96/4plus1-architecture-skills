# Architecture Modeling Instructions

Use these instructions in OpenCode when the user asks for 4+1 architecture modeling, UML sequence diagrams, context modeling, architecture consistency review, or logic-code-deployment traceability.

## Rule Selection

Before answering, match the user's task to one or more local guides:

- Context model: read `docs/architecture-skills/context-model.md`.
- UML sequence diagram: read `docs/architecture-skills/uml-sequence-diagram.md`.
- 4+1 architecture view: read `docs/architecture-skills/4plus1-architecture-view.md`.
- Logic-code-deployment trace: read `docs/architecture-skills/logic-code-deployment-trace.md`.
- Architecture consistency check: read `docs/architecture-skills/architecture-consistency-check.md`.

If multiple apply, use this order:

1. Context model
2. UML sequence diagram
3. 4+1 architecture view
4. Logic-code-deployment trace
5. Architecture consistency check

## Operating Principles

- Start from the original architectural need, not from diagram mechanics.
- If the system boundary or goal is unclear, ask for clarification before drawing.
- If the goal is clear but the requested path is inefficient, explain the shorter path and proceed with the better workflow.
- Prefer diagrams plus trace tables over prose-only answers.
- Always state assumptions, gaps, and model consistency risks.
- For reviews, lead with findings ordered by severity.

## Prompt Examples

```text
Use the architecture modeling instructions to draw a context model for an enterprise approval system.
```

```text
Use the UML sequence diagram guide to model the reimbursement approval and payment flow, including failure branches.
```

```text
Use the 4+1 architecture view guide to produce a draft architecture for this SaaS system.
```

```text
Use the logic-code-deployment trace guide to map these services to repos, build outputs, delivery packages, and Kubernetes deployments.
```

```text
Use the architecture consistency check guide to review this model and list P1/P2/P3 issues.
```
