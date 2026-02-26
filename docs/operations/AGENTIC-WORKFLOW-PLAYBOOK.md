# Agentic Workflow Playbook

## Purpose

This playbook defines the standard operational workflow for implementing changes
in this repository using:

- Planner Agent
- Implementer Agent
- Reviewer Agent
- Structured Handoffs

This workflow enforces:

- ADR compliance
- Prompt Governance Convention
- Layer discipline
- Multi-tenancy invariants
- Security and secret management constraints

Architecture > Prompt > Code.

---

# Core Philosophy

We do NOT:

- Jump directly to implementation.
- Let Copilot generate uncontrolled code.
- Fix architecture after the fact.

We DO:

1. Plan.
2. Implement.
3. Review.
4. Fix (if needed).
5. Move forward.

This is a closed-loop governance system.

---

# Roles Overview

## 1. Planner Agent

Responsibility:
- Analyze request.
- Read relevant ADRs and documentation.
- Produce a structured execution plan.
- Define scope and non-goals.
- Produce a Reviewer Checklist.

Planner never writes code.

---

## 2. Implementer Agent

Responsibility:
- Execute the approved plan.
- Modify files.
- Respect all ADRs.
- Enforce layering and multi-tenancy.
- Provide summary of changes.

Implementer never changes ADRs.

---

## 3. Reviewer Agent

Responsibility:
- Audit changes.
- Detect ADR violations.
- Detect layering violations.
- Detect secret exposure.
- Detect scaling issues.
- Produce structured compliance report.

Reviewer never edits code.

---

# Standard Workflow

For any new step (e.g., STEP-01, STEP-02, feature, refactor):

---

## Phase 1 — Planning

### Step 1: Invoke Planner Agent

Ask Planner:

- Reference relevant ADRs.
- Reference STEP document (if exists).
- Produce plan.

Planner outputs:

- Architectural overview
- Execution steps
- Layer impact
- Risks
- Non-goals
- Reviewer checklist

---

## Phase 2 — Implementation

### Step 2: Handoff to Implementer

Use the built-in handoff:

Planner → Implementer

Implementer:

- Reads plan.
- Applies changes.
- Modifies files.
- Runs checks if necessary.
- Produces summary of changes.

---

## Phase 3 — Review

### Step 3: Handoff to Reviewer

Use handoff:

Implementer → Reviewer

Reviewer:

- Audits repository.
- Checks ADR compliance.
- Checks layering discipline.
- Checks secret exposure.
- Produces structured report.

---

## Phase 4 — Correction (If Needed)

If Reviewer reports violations:

Reviewer → Implementer (handoff)

Implementer fixes issues.

Cycle continues until compliant.

---

# Example: STEP-01 Bootstrap

## 1. Planner

Input:
- STEP-01-monorepo-bootstrap.md
- ADR-001, ADR-002, ADR-009

Output:
- Structured bootstrap plan.
- Clear non-goals (no Celery, no JWT, etc.).
- Reviewer checklist.

---

## 2. Implementer

Executes:
- Django project initialization.
- Layer folder creation.
- Placeholder modules.
- Settings restructuring.

Produces:
- File list.
- Justification aligned with ADRs.

---

## 3. Reviewer

Checks:
- Domain does not import Django.
- No secrets introduced.
- Stateless discipline preserved.
- No circular dependencies.

Outputs:
- Compliance report.

If clean → proceed to STEP-02.

---

# Handoff Discipline

Every handoff MUST contain:

1. Current state.
2. Active ADR constraints.
3. Output of previous agent.
4. Objective for next agent.
5. Non-goals.

No ambiguous transitions.

If ambiguity exists:
Next agent must request clarification.

---

# When to Use Each Agent

| Scenario | Agent |
|----------|-------|
| New feature | Planner |
| Refactor | Planner |
| Architecture-sensitive change | Planner |
| Execute structured step | Implementer |
| Validate compliance | Reviewer |
| Fix violations | Implementer (after Reviewer) |

---

# Anti-Patterns (Forbidden)

- Skipping Planner for non-trivial changes.
- Letting Implementer decide architecture.
- Ignoring Reviewer findings.
- Overriding ADR implicitly.
- Hardcoding secrets.
- Adding cross-layer imports.

---

# Enforcement Loop

Every non-trivial change must go through:

Planner → Implementer → Reviewer

This is mandatory for:

- New modules
- DB changes
- Background jobs
- Authentication changes
- Infrastructure changes
- Multi-tenancy logic

---

# Governance Escalation

If repeated violations occur:

1. Stop implementation.
2. Re-read relevant ADR.
3. Update Planner constraints.
4. Restart from Planner phase.

Never patch around architecture.

---

# Minimal vs Full Workflow

Small cosmetic changes:
- May skip Planner.
- Still use Reviewer.

Architectural or structural changes:
- Always use full workflow.

---

# Definition of Done

A change is considered complete only when:

- Reviewer reports no architectural violations.
- No secrets introduced.
- No layer violations.
- Multi-tenancy preserved.
- Scaling discipline preserved.
- Code compiles and runs.

---

# Integration with Operational Steps

For each STEP-XX:

1. Read STEP document.
2. Use Planner.
3. Handoff to Implementer.
4. Handoff to Reviewer.
5. Only then move to next STEP.

---

# Final Reminder

This repository is governed by ADRs.

Agents are tools.
Architecture is the law.