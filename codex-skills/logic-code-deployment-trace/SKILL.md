---
name: "logic-code-deployment-trace"
description: "Use when mapping or auditing traceability from logical architecture elements to code repositories/directories, build outputs, delivery packages, and deployment targets in a 4+1 architecture model."
---

# Logic-Code-Deployment Trace

Use this skill to make architecture traceability explicit across logical, development, build, delivery, and deployment models.

Reference basis: Huawei Cloud CodeArts Modeling software modeling guide, logical/development/deployment view and traceability concepts. Original vendor PDF is not redistributed with this project.

## Trace Chain

Build the chain in this direction:

```text
Use Case / Scenario
-> Logical element: System, SubSystem, Service, Component, MicroService, Module
-> Code element: Repo Group, Repo, Dir, File
-> Build element: Exec Target, Compile Target, tools, build environment
-> Delivery element: Release, Delivery Target, packaged third-party or OS dependency
-> Deployment element: Node, Zone, Execution Environment, Process, Processing Unit, FRU
-> Runtime interaction: process or service collaboration when needed
```

## Relationship Semantics

Use the relationship that matches the trace:

- Code element -> logical element: `Manifest`.
- Build element -> code element: `Build From`.
- Delivery target contains build output or external software: `Composition` or `Aggregation`.
- Delivery target or executable target -> deployment element: `Deployed To`.
- Deployment communication path: `CommunicationPath`.
- Logical decomposition: `Composition` or `Aggregation`.

Direction matters when the modeling tool distinguishes it. Preserve the source-to-target convention above.

## Workflow

1. Start with logical elements that are architecture-owned and implementable.
2. For each Service, MicroService, or Component, identify the owning repository, directory, or file.
3. Add Manifest links from code elements to logical elements.
4. Identify build outputs for each code element and add Build From links.
5. Identify delivery packages and releases; show what build outputs and external software they contain.
6. Identify deployment targets and link executable or delivery targets to nodes, execution environments, processes, or zones.
7. Add runtime interactions only for startup, critical flows, cross-process calls, or operationally important behavior.
8. Produce a gap report before drawing extra detail.

## Gap Types

Flag these explicitly:

- Logical element has no code Manifest.
- Code element maps to multiple logical elements without an intentional grouping explanation.
- Repo exists but no concrete repository is configured.
- Build target has no Build From source.
- Delivery target does not contain any build output.
- Executable or delivery target is not deployed anywhere.
- Deployment node has no artifact.
- Runtime interaction references a logical element not present in the logical model.

## Output Format

Provide a trace table:

```text
Scenario | Logical element | Code | Build output | Delivery target | Deployment target | Runtime note | Gaps
```

Then provide:

- Diagram code or modeling instructions.
- Highest-risk gaps first.
- Assumptions about repositories, build outputs, packages, and deployment topology.

## Validation Checklist

- Every required logical element has at least one code mapping.
- Every build output traces back to code.
- Every delivery artifact traces back to build outputs or declared external software.
- Every deployable artifact has a deployment target.
- Relationship names and directions are consistent.
- The trace table can be used to answer "where is this design implemented, built, packaged, and deployed?"
