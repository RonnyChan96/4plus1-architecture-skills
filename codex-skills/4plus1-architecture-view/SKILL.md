---
name: "4plus1-architecture-view"
description: "Use when drawing or reviewing a software 4+1 architecture view set: use-case, logical, development, deployment, and runtime views, especially when the work should follow Huawei CodeArts Modeling 4+1 view conventions."
---

# 4+1 Architecture View

Use this skill to produce a coherent 4+1 architecture model from requirements, codebase facts, existing diagrams, or stakeholder notes.

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

1. Use-case view
   - Context model: system boundary, actors, external systems, interfaces.
   - Use-case model: key business use cases and architecture-significant interaction scenarios.
   - Use UML sequence diagrams for complex interactions.
2. Logical view
   - Logical model: system decomposition and relationships.
   - Data model: required for data-heavy systems.
   - Domain model and function model: optional when they clarify business concepts or feature decomposition.
   - Technical model: key frameworks, infrastructure, common mechanisms, and technical components.
3. Development view
   - Code model: repositories, directories, files, and their mapping to logical elements.
   - Build model: build outputs, tools, environments, platforms, and source relationships.
4. Deployment view
   - Delivery model: release offerings and delivery targets built from executable targets and external software.
   - Deployment model: deployment targets, nodes, execution environments, processes, and deployed artifacts.
5. Runtime view
   - Runtime model: startup, runtime interaction, process-level collaboration, and key data flows.
   - Optional, but include it when interactions, concurrency, startup order, or operational behavior are architecture-significant.

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

Prefer Mermaid for lightweight communication and PlantUML when UML precision matters. If the user is working in CodeArts Modeling, phrase steps in terms of model types and relationship names.

## Validation Checklist

Before finalizing:

- One system boundary is clear.
- Key actors and external systems are represented in the context model.
- Architecture-significant use cases drive the design.
- Logical decomposition reaches implementable ownership granularity.
- Relationships are modeled, not implied in prose.
- Code, build, delivery, deployment, and runtime views reuse or reference upstream elements instead of recreating them independently.
- Traceability gaps are called out explicitly.
