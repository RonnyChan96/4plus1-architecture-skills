# Architecture Consistency Check

Use this guide to review architecture models, diagrams, or diagram-as-code for consistency issues before they become documentation drift.

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

## Key Rules By View

- Logical model: no orphaned elements, no duplicate same-level same-type siblings, logical-to-logical structural relations should use Composition or Aggregation, logical-to-interface relations should use Usage, Dependency, or Realization.
- Technical model: technical elements should follow hierarchy and connect to logical elements through technical-realizes-logical or logical-uses/depends-on-technical relationships.
- Code model: repos should be configured; code-to-logical mapping should use Manifest; Service, MicroService, and Component elements should have at least one Manifest from a code element.
- Build model: build elements should relate to code elements using Build From.
- Delivery model: build elements and delivery elements should use Composition or Aggregation.
- Deployment model: delivery targets and executable targets must be deployed to at least one deployment element through Deployed To or valid containment.
- Context model: exactly one System; Actor and ExternalSystem should interact with System through interfaces, not direct lines.
- Runtime model: reference or instantiate logical elements; do not create new logical elements.

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
