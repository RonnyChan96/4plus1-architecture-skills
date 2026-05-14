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
   - Context model: system boundary, actors, external systems, interfaces. Do not expand internal system components in the context model.
   - Use-case model: key business use cases and architecture-significant interaction scenarios. Actors must be referenced from the context model, not newly created in the use-case model.
   - Use UML sequence diagrams for complex interactions.
2. Logical view
   - Logical model: system decomposition and relationships. Include at least a 0-level and 1-level logical model.
   - Data model: required for data-heavy systems.
   - Domain model and function model: optional when they clarify business concepts or feature decomposition.
   - Technical model: databases, middleware, frameworks, operating systems, platforms, infrastructure, common mechanisms, and technical components.
3. Development view
   - Code model: repositories, directories, files, and their Manifest mapping to referenced logical elements.
   - Build model: build outputs, tools, environments, platforms, and Build From source relationships to referenced code elements.
4. Deployment view
   - Delivery model: Release, Dlvr Trgt, Exec Trgt, ThirdParty, operating systems, package tools, and package composition.
   - Deployment model: Node, ExecEnv, Process, Zone, communication paths, and deployed artifacts.
5. Runtime view
   - Runtime model and runtime sequence diagram: startup, runtime interaction, process-level collaboration, and key data flows.
   - The runtime sequence diagram is required for a complete 4+1 output. Lifelines must come from context model Actor/ExternalSystem or logical model objects; do not invent participants that do not belong to preceding views.

## Logical Granularity

Pick the decomposition level that can guide implementation and ownership:

- Service-oriented systems: use Service and MS (MicroService); model at least to MicroService level when microservices are the deployable ownership unit.
- Componentized systems: use Component; model at least to Component level.
- Modular systems: use Module; model at least to Module level.
- Use Domain, Layer, and Plane only as grouping or auxiliary expression. They must not replace implementable architecture objects such as Service, MS, Component, or Module.

Avoid stopping at vague concepts or feature buckets. Avoid over-modeling below module level unless the user explicitly needs detailed design.

## Modeling Rules

- Context model only contains Actor, System, ExternalSystem, and Interface-like elements. It must not decompose the System into internal services, components, modules, databases, middleware, or deployment nodes.
- In context models, System interaction with Actor or ExternalSystem is expressed through Interface plus Usage, Realization, and where the modeling convention requires it, Association. Do not use context diagrams as internal architecture diagrams.
- In use-case models, Actor elements must come from the context model. Do not create new Actor elements in the use-case model. Actor-to-UseCase interaction uses Use; UseCase-to-UseCase relationships may use Include and Extend.
- Logical view must include at least two logical model levels:
  - 0-level: shows System and SubSystem; it may omit detailed relationships when used for broad communication.
  - 1-level: must show architecture objects and relationships.
- Logical elements are the baseline for development, deployment, and runtime views.
- Separate business logical model and technical model. Logical model expresses business function parts; databases, middleware, frameworks, operating systems, platforms, and infrastructure belong in the technical model.
- In code models, logical elements must be referenced from the logical model; do not recreate them in the code model.
- Development view must map code elements to logical elements with Manifest relationships. Manifest direction is code element -> logical element.
- In build models, code elements must be referenced from the code model; do not recreate code elements in the build model.
- Build model must map build outputs to code elements with Build From relationships. Build From direction is build element -> code element.
- Deployment view is split into delivery model and deployment model:
  - Delivery model uses Release, Dlvr Trgt, Exec Trgt, ThirdParty, OperatingSystem, Package Tools, Composition, and Aggregation.
  - Deployment model uses Node, ExecEnv, Process, Zone, Deployed To, and CommunicationPath.
- Deployment model must map executable or delivery targets to deployment elements with Deployed To or valid containment relationships. CommunicationPath expresses deployment communication routes.
- Runtime sequence diagram lifelines must be reused from the context or logical model. Runtime views may reference or instantiate existing logical elements, but should not create new logical elements.

## Output Structure

When producing a result, include:

- A view inventory: which diagrams/models are included and why.
- Diagram code or modeling instructions for each included view.
- A trace summary linking scenarios -> logical elements -> code/build -> delivery/deployment -> runtime interactions.
- A CodeArts relationship mapping that names which diagram edges must be created as Usage, Realization, Association, Use, Include, Extend, Manifest, Build From, Deployed To, or CommunicationPath.
- A short consistency checklist with gaps and assumptions.

Prefer Mermaid for lightweight communication and PlantUML when UML precision matters. If the user is working in CodeArts Modeling, phrase steps in terms of model types and relationship names.

For Mermaid output, label nodes with CodeArts semantic stereotypes, for example:

- `«System» Approval System`
- `«Actor» Employee`
- `«ExternalSystem» Bank Payment API`
- `«Service» Approval Service`
- `«MS» Notification MS`
- `«Component» Rule Engine`
- `«Module» Approval Domain Module`
- `«Dir» src/approval`
- `«Exec Trgt» approval-service.jar`
- `«Dlvr Trgt» approval-release.tar.gz`
- `«Node» k8s-worker-01`
- `«ExecEnv» Kubernetes Namespace`
- `«Process» approval-service`

After each Mermaid diagram, add a short note mapping visual edges to CodeArts relationship types, especially Usage, Realization, Association, Manifest, Build From, Deployed To, and CommunicationPath.

## Validation Checklist

Before finalizing:

- One system boundary is clear.
- Key actors and external systems are represented in the context model.
- Context model does not show internal system services, components, modules, databases, middleware, or deployment nodes.
- Use-case model actors are referenced from the context model.
- Architecture-significant use cases drive the design.
- Logical view includes both 0-level and 1-level logical models.
- Logical decomposition reaches implementable ownership granularity.
- Business logical elements are separated from technical infrastructure elements.
- Relationships are modeled, not implied in prose.
- Manifest direction is code element -> logical element.
- Build From direction is build element -> code element.
- Runtime sequence diagram lifelines come from context or logical model objects.
- Code, build, delivery, deployment, and runtime views reuse or reference upstream elements instead of recreating them independently.
- Traceability gaps are called out explicitly.
