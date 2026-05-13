---
name: "architecture-consistency-check"
description: "Use when checking 4+1 architecture model consistency: hierarchy rules, orphan elements, duplicate siblings, allowed relationships, context model rules, code manifest links, build links, delivery links, deployment links, and runtime model rules."
---

# Architecture Consistency Check

Use this skill to review architecture models, diagrams, or diagram-as-code for consistency issues before they become documentation drift.

Reference basis: Huawei Cloud CodeArts Modeling software modeling guide, architecture consistency check concepts. Original vendor PDF is not redistributed with this project.

## Review Method

Check from structural basics to cross-view traceability:

1. Basic model hygiene.
2. Per-view hierarchy and orphan rules.
3. Relationship type rules.
4. Cross-view realization and traceability.
5. Fix guidance with exact offending elements and suggested relationship changes.

Report findings first. Use severity:

- P1: broken traceability or wrong relationship that invalidates the model.
- P2: missing required element, orphan, duplicate, or hierarchy violation.
- P3: naming, clarity, or optional completeness issue.

## Common Rules

- Element names must not be empty.
- Elements in a model tree must match the configured hierarchy for that view.
- No architecture element should be orphaned outside the view's architecture tree.
- Siblings under the same parent should not have the same name and same type.
- Containment/decomposition should use allowed structural relations such as Composition or Aggregation where the view expects hierarchy.

## Logical Model Rules

- Logical elements must follow the intended hierarchy.
- Logical elements must not be orphaned.
- Same-level same-parent logical elements must not duplicate name and type.
- Logical-to-logical structural relationships should use Composition or Aggregation.
- Logical elements and interfaces should use Usage, Dependency, or Realization.
- Interface-to-interface structural relationships should use Composition or Aggregation.

## Technical Model Rules

- Technical elements must follow the technical hierarchy and not be orphaned.
- Same-level same-parent technical elements must not duplicate name and type.
- Technical elements and logical elements should be connected by technical-realizes-logical or logical-uses/depends-on-technical relationships.

## Code And Build Rules

- Code elements must follow the code model hierarchy and not be orphaned.
- Same-level same-parent code elements must not duplicate name and type.
- Repo elements should be configured with an actual repository.
- Code elements and logical elements should only use Manifest for implementation mapping.
- One code element should map to one logical element unless the model explicitly uses a grouping element.
- Service, MicroService, and Component logical elements should have at least one Manifest relationship from a code element.
- Build elements must follow build hierarchy and not be orphaned.
- Build elements should relate to code elements using Build From.

## Delivery And Deployment Rules

- Delivery elements must follow delivery hierarchy and not be orphaned.
- Same-level same-parent delivery elements must not duplicate name and type.
- Build elements and delivery elements should use Composition or Aggregation.
- Deployment elements must follow deployment hierarchy and not be orphaned.
- Same-level same-parent deployment elements must not duplicate name and type.
- Delivery targets and executable targets must be deployed to at least one deployment element through Deployed To or valid containment.

## Context And Runtime Rules

- A context model should contain exactly one System.
- Actor and ExternalSystem should interact with System through interfaces, not by direct actor-system lines.
- Valid context interaction patterns:
  - Actor or ExternalSystem realizes an interface; System uses or depends on it.
  - System realizes an interface; Actor or ExternalSystem uses or depends on it.
- Runtime models, runtime sequence diagrams, and runtime activity diagrams should reference or instantiate logical elements; they should not create new logical elements.

## Output Format

For each finding:

```text
[Severity] Rule: <short rule name>
Evidence: <element/relationship/diagram>
Why it matters: <impact>
Fix: <specific modeling change>
```

Then include:

- Cross-view traceability summary.
- Unchecked assumptions.
- Minimal next actions.

## Validation Checklist

- Findings are grounded in named elements or relationships.
- Fixes specify the replacement relation or missing link.
- Cross-view gaps are separated from local diagram style issues.
- The review does not invent missing model facts; unknowns are listed as assumptions.
