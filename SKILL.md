---
name: greenfield-architecture-planner
description: Plan the architecture for a brand-new software project from product specs, acceptance criteria, constraints, and project principles. Use when choosing stack, service boundaries, data model, API contracts, UI architecture, security posture, deployment shape, observability, and validation strategy before bootstrapping or implementation.
metadata:
  dispatcher-category: architecture
  dispatcher-layer: information
  dispatcher-lifecycle: draft
  dispatcher-risk: medium
  dispatcher-writes-files: true
  dispatcher-capabilities: greenfield-architecture-planning, stack-selection, architecture-decisions, data-modeling, api-planning, deployment-planning
  dispatcher-accepted-intents: plan_greenfield_architecture, create_architecture_plan, select_project_architecture
  dispatcher-input-artifacts: product_spec, acceptance_criteria, project_constitution, constraints, stack_preference
  dispatcher-output-artifacts: architecture_plan, decision_log, data_model, api_contract_outline, validation_strategy
  dispatcher-stack-tags: architecture, greenfield, api, frontend, backend, deployment
---

# Greenfield Architecture Planner

Use this skill after the product scope and acceptance criteria are clear enough to make technical decisions.

This skill produces an architecture plan. It does not bootstrap the repository and does not implement code.

## Outcomes

- Select a right-sized architecture for a new project.
- Capture stack decisions and trade-offs.
- Define system boundaries, modules, data model, API contracts, UI architecture, security posture, deployment shape, observability, and validation strategy.
- Produce a plan that `implementation-task-planner-skill` can turn into executable tasks.

## Do Not Use This Skill For

- Coding the project.
- Creating framework scaffolds. Use `project-bootstrapper-skill`.
- Generating full backlog packs. Use `backlog-story-generator`.
- Auditing an existing production codebase. Use `principal-audit-refactor`.

## Workflow

0. Log telemetry if available:

```bash
%USERPROFILE%\.agents\skills\skill-dispatcher\log-dispatch.cmd --skill greenfield-architecture-planner --intent plan_greenfield_architecture --model <model_name> --reason <reason>
```

1. Read the product spec, acceptance criteria, constitution, and constraints.
2. Identify the MVP boundary and expected first vertical slice.
3. List candidate architecture options only when there is a real decision to make.
4. Select the recommended architecture and explain why it fits the constraints.
5. Define boundaries:
   - frontend or interface layer
   - backend or service layer
   - persistence layer
   - integration boundaries
   - background jobs or asynchronous workflows
6. Define the data model at conceptual and implementation levels.
7. Define API or event contracts at outline level. Use `openapi-spec-generation` downstream when a full OpenAPI contract is needed.
8. Define security, privacy, accessibility, observability, and performance considerations.
9. Define deployment and local development shape.
10. Define validation strategy by test layer.
11. Save the plan only when the chain or user requested file artifacts.

## Current-Information Rule

If the plan depends on fast-changing versions, cloud services, library capabilities, or framework recommendations, verify against official documentation or primary sources before stating version-specific guidance.

## Output Contract

Use this structure:

```markdown
# Architecture Plan: <project-name>

## Executive Summary
## Inputs Reviewed
## Architecture Drivers
## Recommended Architecture
## Alternatives Considered
## System Boundaries
## Data Model
## API and Integration Contracts
## UI Architecture
## Security and Privacy
## Accessibility and UX Constraints
## Observability and Operations
## Deployment and Local Development
## Validation Strategy
## Decision Log
## Risks and Open Questions
## Handoff To Task Planning
```

## Decision Log Format

```markdown
| ID | Decision | Status | Rationale | Consequences |
| --- | --- | --- | --- | --- |
| ADR-001 | Use <stack> | Proposed | <why> | <trade-off> |
```

## Handoff Requirements

End with a clear section for `implementation-task-planner-skill`:

- target stack and package manager
- source directories expected
- major modules to create
- contracts to implement
- test layers required
- first vertical slice
- validation commands when known

## Guardrails

- Do not invent user requirements to justify architecture choices.
- Do not over-engineer a small project with distributed systems, queues, or microservices unless constraints require them.
- Do not choose a stack that conflicts with explicit user preferences without explaining the conflict.
- Do not make security or data-retention claims without source requirements.
- Do not generate full implementation tasks. Leave that to `implementation-task-planner-skill`.

## Final Response

Report:

- architecture plan path if saved
- recommended stack and rationale
- key decisions
- unresolved questions
- next skill to invoke
