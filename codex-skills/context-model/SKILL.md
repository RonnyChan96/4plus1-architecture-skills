---
name: "context-model"
description: "Use when drawing or reviewing a 4+1 context model that defines a system boundary, actors, external systems, interfaces, and interface-mediated interactions."
---

# Context Model

Use this skill to define the system boundary before deeper architecture design.

Reference basis: Huawei Cloud CodeArts Modeling software modeling guide, context model concepts. Original vendor PDF is not redistributed with this project.

## Purpose

A context model answers:

- What is the system?
- Who or what is outside it?
- Which interfaces cross the boundary?
- What is inside the architecture scope and what is not?

Do this before use-case, logical, development, deployment, or runtime modeling when the boundary is unclear.

## Elements

Use:

- `System`: the system being designed. Use exactly one in a context model.
- `Actor`: a person, role, organization, or external participant interacting with the system.
- `ExternalSystem`: another system, device, service, platform, or third-party dependency.
- `Boundary`: optional grouping for scope or environment.
- `Interface`: a named interaction contract.
- `ProvidedInterface`: interface provided by an element.
- `RequiredInterface`: interface required by an element.
- `Realization`: element implements/provides an interface.
- `Usage` or `Dependency`: element uses/depends on an interface.
- `Association`: only when the modeling convention explicitly permits it for non-boundary ownership; do not use it as a shortcut for actor-system interaction.

## Core Rule

Do not connect Actor or ExternalSystem directly to System to express interaction. Model interaction through interfaces:

- System provides an interface, and Actor or ExternalSystem uses or depends on it.
- Actor or ExternalSystem provides an interface, and System uses or depends on it.

If the System already exists in the logical model, reference it into the context model instead of creating a duplicate.

## Workflow

1. Name the System in business terms.
2. List external actors and external systems from requirements, integrations, users, operators, devices, and platforms.
3. Decide which external participants are in scope for the current scenario or product boundary.
4. Name each boundary-crossing interface by capability or protocol.
5. Connect participants through interface realization and usage/dependency.
6. Split into multiple context diagrams if there are too many external participants; split by actor class, integration group, or deployment scenario.
7. Validate that the context model supports the use-case model and does not duplicate logical model elements.

## Output Expectations

Include:

- Context diagram code or modeling instructions.
- Table of external participants and why each is outside the system.
- Interface table with provider, consumer, purpose, and assumptions.
- Boundary decisions and open questions.

Prefer a simple component-style diagram for communication, and PlantUML/UML notation when exact interface relations matter.

## Validation Checklist

- Exactly one System is present.
- Every Actor or ExternalSystem interaction crosses an Interface.
- Interfaces have meaningful names.
- Boundary includes only the system under design.
- External participants are not modeled as internal logical components.
- Missing or ambiguous ownership is listed as an open question.
