# 4+1 Architecture View

Use this guide to produce a coherent 4+1 architecture model from requirements, codebase facts, existing diagrams, or stakeholder notes.

Reference basis: Huawei Cloud CodeArts Modeling software modeling guide, 4+1 architecture view concepts. Original vendor PDF is not redistributed with this project.

## First Principles

Start from the system boundary and stakeholder questions:

- What is the system, and what is outside it?
- Which scenarios drive architecture decisions?
- What logical parts satisfy those scenarios?
- Which repositories, build outputs, delivery packages, and deployment nodes realize those parts?
- Which runtime interactions validate the design?

Do not draw five disconnected diagrams. The "+1" use-case view drives and validates the other four views.

## Required Views

Create or review the views in this order:

1. Use-case view: context model, use-case model, key sequence diagrams.
2. Logical view: logical model, data model for data-heavy systems, optional domain/function models, technical model.
3. Development view: code model and build model.
4. Deployment view: delivery model and deployment model.
5. Runtime view: startup, runtime interaction, process collaboration, and key data flows when architecture-significant.

## Logical Granularity

Pick the decomposition level that can guide implementation and ownership:

- Componentized systems: model at least to Component level.
- Service-oriented systems: model at least to MicroService level.
- Modular systems: model at least to Module level.

Avoid stopping at vague concepts or feature buckets. Avoid over-modeling below module level unless the user explicitly needs detailed design.

## Modeling Rules

- The 0-level logical model may focus on major parts and omit detailed relationships when used for broad communication.
- Lower-level logical models should show both architecture elements and relationships.
- Logical elements are the baseline for development, deployment, and runtime views.
- Development view must map logical elements to code elements with Manifest relationships.
- Build model must map build outputs to code elements with Build From relationships.
- Deployment model must map executable or delivery targets to deployment elements with Deployed To or containment relationships.
- Use technical model for technology choices and technical support elements; keep business logical decomposition separate from implementation technology where possible.

## Output Structure

When producing a result, include:

- A view inventory: which diagrams/models are included and why.
- Diagram code or modeling instructions for each included view.
- A trace summary linking scenarios -> logical elements -> code/build -> delivery/deployment -> runtime interactions.
- A short consistency checklist with gaps and assumptions.

Prefer Mermaid for lightweight communication and PlantUML when UML precision matters.

## Validation Checklist

- One system boundary is clear.
- Key actors and external systems are represented in the context model.
- Architecture-significant use cases drive the design.
- Logical decomposition reaches implementable ownership granularity.
- Relationships are modeled, not implied in prose.
- Code, build, delivery, deployment, and runtime views reuse or reference upstream elements instead of recreating them independently.
- Traceability gaps are called out explicitly.
