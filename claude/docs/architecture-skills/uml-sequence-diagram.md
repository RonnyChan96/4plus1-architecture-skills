# UML Sequence Diagram

Use this guide to model interaction behavior precisely enough to reveal hidden requirements, constraints, ordering, error handling, and runtime responsibilities.

Reference basis: Huawei Cloud CodeArts Modeling software modeling guide, UML sequence diagram concepts. Original vendor PDF is not redistributed with this project.

## Start From Behavior

Identify:

- Triggering use case or runtime scenario.
- Participants: actor, external system, system, service, component, process, or execution target.
- Main success path.
- Branches, loops, parallel work, retries, timeouts, and failures.
- Data or message payloads that affect architecture decisions.

Only include participants that exchange messages in this scenario. Do not use a sequence diagram as a component inventory.

## Diagram Elements

Use:

- Lifeline for each participant.
- Message lines for calls, events, responses, creates, destroys, or asynchronous notifications.
- Activation bars for execution periods when they clarify responsibility or nested calls.
- Combined fragments for control logic.
- Diagram gates when a message enters or exits a referenced interaction or fragment boundary.

Use participant names that match the surrounding 4+1 model where possible. Actors should come from the context/use-case model. Internal participants should come from logical, deployment, or runtime models.

## Combined Fragments

Choose the operator by meaning:

- `alt`: if/else-if/switch-style alternatives.
- `opt`: optional single branch.
- `break`: interrupt remaining behavior when the guard is true.
- `loop`: repeated behavior.
- `par`: parallel behavior.
- `critical`: non-interleavable section inside parallel or ordered behavior.
- `seq`: weak ordering where unrelated lifelines may interleave.
- `strict`: strict ordering across operands.
- `consider`: only listed messages are relevant.
- `ignore`: listed messages are intentionally omitted.
- `assert`: the only valid sequence.
- `neg`: invalid sequence that must not happen.

Every guarded fragment should have concise, testable guard text.

## Workflow

1. Write the scenario title as an observable behavior.
2. List participants and map them to existing model elements when available.
3. Draw the main path first.
4. Add return messages only when they clarify data flow or decision points.
5. Add activation bars for nested responsibility or long-running work.
6. Add fragments for branches, loops, interruption, and concurrency.
7. Check whether each message has a clear sender, receiver, trigger, and architectural purpose.
8. Cross-check the diagram against code or requirements if available.

## Output Expectations

Prefer PlantUML for UML sequence diagrams. Mermaid is acceptable for quick communication when fragment support is sufficient.

Include:

- Diagram code.
- Participant-to-model mapping.
- Assumptions and omitted detail.
- Validation notes for ambiguous ordering, missing error paths, or participants not present in the architecture model.

## Validation Checklist

- The diagram describes one scenario, not an entire system.
- Lifelines are necessary and named consistently.
- Message order matches the scenario.
- Branches and loops use explicit guards.
- Error and timeout paths are represented when architecture-significant.
- The sequence can be traced back to a use case or runtime concern.
