# Prompt Governance Convention

## Purpose

This document defines the rules, structure, lifecycle, and governance model for prompts used with GitHub Copilot Chat (VS Code) within this project.

Prompts are treated as:

- Architectural artifacts
- Version-controlled assets
- Execution blueprints
- Governance-enforcing instruments

Prompts are not disposable text.
They are part of the platform’s operational discipline.

---

# Core Principle

Prompts must enforce architecture, not bypass it.

If a prompt generates code that violates ADR invariants,
the prompt must be corrected.

Architecture > Prompt > Code

---

# Folder Structure

All prompts must live inside:

docs/prompts/

Recommended structure:

docs/prompts/
│
├── operational/
│   ├── step-01/
│   ├── step-02/
│   └── ...
│
├── governance/
│   ├── layer-validation/
│   ├── tenant-isolation-check/
│   └── security-audit/
│
├── reusable/
│
└── experiments/

Prompts must never live outside version control.

---

# Prompt Structure Standard

Every prompt file must follow this structure:

# Prompt Title

## Objective
Clear description of what must be achieved.

## Related ADR
Explicit list of ADRs this prompt must comply with.

## Architectural Constraints
Explicit invariants that Copilot must respect.

## Tasks
Step-by-step execution instructions.

## Non-Goals
Explicitly state what must NOT be implemented.

## Expected Output
Describe structure or behavior expected.

## Post-Execution Validation
Instructions for verifying compliance.

---

# Mandatory Architectural References

Every operational prompt must explicitly reference:

- ADR-001 (Tenant Isolation)
- ADR-002 (Database Strategy)
- ADR-009 (Scaling discipline)

If relevant, also reference:

- ADR-006 (Background Jobs)
- ADR-011 (Event-Driven Architecture)
- ADR-012 (Tracing)
- ADR-014 (Secret Management)

Prompts that do not declare ADR references are invalid.

---

# Layer Protection Rules

Prompts must enforce:

1. Domain must not import infrastructure.
2. Infrastructure may depend on domain.
3. Interfaces must not contain business logic.
4. No cross-layer shortcuts.
5. No secrets hardcoded.
6. Tenant context must be explicit.

If Copilot suggests violating these rules, the suggestion must be rejected.

---

# Copilot Mode Discipline

For each prompt, explicitly declare the mode to use:

- Ask Mode → architectural clarification.
- Edit Mode → controlled file modifications.
- Agent Mode → multi-file autonomous implementation.
- Plan Mode → design before implementation.

Operational prompts must specify the intended mode.

---

# Versioning & Evolution

Prompt changes must:

- Be committed with meaningful message.
- Explain what was improved.
- Reference affected ADR if relevant.

If a prompt contradicts an ADR:
- Update the prompt.
- Do not silently override architecture.

---

# Validation Checklist After Execution

After Copilot execution, verify:

- No cross-layer imports.
- No circular dependencies.
- Tenant isolation preserved.
- No secret exposure.
- Code compiles.
- Architecture respected.

If violation detected:
- Fix immediately.
- Update prompt to prevent recurrence.

---

# Governance Escalation Rule

If implementation repeatedly violates ADR discipline:

1. Stop implementation.
2. Review related ADR.
3. Adjust prompt.
4. Re-run with stricter constraints.

Never “patch around” architectural violations.

---

# Architectural Hierarchy

ADR → Prompt Governance → Prompt → Implementation

This hierarchy must never be inverted.

---

# Final Rule

Prompts are executable architecture.

Treat them with the same rigor as:

- Database migrations
- Security policies
- Cryptographic decisions