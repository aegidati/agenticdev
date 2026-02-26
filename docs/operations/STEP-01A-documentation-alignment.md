# STEP-01A — Documentation Alignment (Architecture ↔ ADR)

## 1. Purpose

This STEP ensures strict structural and semantic alignment between:

- docs/adr/
- docs/architecture/

The objective is to:

- Eliminate duplication between ADRs and architecture documents.
- Ensure that all architectural decisions live exclusively in ADRs.
- Ensure that architecture documents describe implementation guidance only.
- Prevent architectural drift.
- Strengthen governance clarity for Planner / Implementer / Reviewer agents.

This STEP is documentation-only.

It MUST NOT:

- Modify runtime behavior.
- Modify source code.
- Introduce new architectural decisions silently.

---

## 2. Scope

### 2.1 In Scope

- All files under:
  - docs/architecture/
  - docs/adr/

- Identification of duplicated normative statements.
- Refactoring architecture documents to reference ADRs.
- Addition of "Related ADRs" section to each architecture file.
- Minor structural improvements for clarity and consistency.

### 2.2 Out of Scope

- backend/
- frontend/
- packages/
- CI/CD configuration
- Agent definitions
- Runtime configuration
- Any modification of architectural decisions inside ADRs
- Creation of new ADRs (unless a missing decision is explicitly discovered and flagged)

---

## 3. Architectural Context

The documentation system follows a layered governance model:

- ADRs define:
  - Decisions
  - Rationale
  - Alternatives
  - Consequences
  - Policy-level constraints (MUST / MUST NOT)

- Architecture documents define:
  - Implementation patterns
  - Folder structures
  - Code examples
  - Operational guidance

This STEP reinforces governance defined in:

- ADR-013 — API Versioning
- ADR-015 — Error & Exception Handling
- ADR-016 — Testing Strategy
- ADR-017 — Dependency Strategy
- ADR-018 — Migration Policy
- ADR-019 — Observability & Logging Contract
- ADR-020 — Code Style Governance

---

## 4. Alignment Rules

The following rules MUST be enforced.

### Rule 1 — Decisions Live in ADRs

If a statement defines a policy or invariant such as:

- "All tenant-scoped tables MUST include tenant_id."
- "All API endpoints MUST be versioned."
- "JWT MUST use RS256."
- "Error responses MUST follow a specific JSON schema."

Then:

- The authoritative definition MUST exist in an ADR.
- Architecture documents MUST reference the ADR.
- Architecture documents MUST NOT redefine the rule as an independent decision.

---

### Rule 2 — Architecture Explains "How"

Architecture documents MAY contain:

- Folder structure examples
- Middleware examples
- Code snippets
- Logging configuration samples
- Request/response examples
- Implementation patterns

Architecture documents MUST NOT introduce new normative constraints.

---

### Rule 3 — Cross-Referencing Is Mandatory

Each file in docs/architecture/ MUST start with:

Related ADRs:
- ADR-0xx — ...
- ADR-0yy — ...

No architecture file may exist without explicit linkage to relevant ADRs.

---

### Rule 4 — No Hidden Decisions

If a true architectural rule is discovered that:

- Does not exist in any ADR
- Is expressed as a MUST-level constraint

Then:

- It MUST be flagged.
- It MUST NOT remain hidden inside architecture documentation.
- A new ADR proposal MAY be required (outside this STEP).

---

## 5. Execution Requirements

The Planner Agent MUST:

1. List all files under docs/architecture/.
2. For each file:
   - Identify duplicated normative statements.
   - Identify decision-level language (MUST, ALWAYS, NEVER).
3. Produce a refactoring plan that:
   - Adds "Related ADRs" section to each architecture file.
   - Replaces duplicated decisions with ADR references.
   - Preserves implementation guidance.
4. Confirm that:
   - No ADR content is substantively modified.
   - No runtime code is impacted.

The Implementer Agent MUST:

- Apply refactoring exactly as planned.
- Avoid semantic alteration of ADR decisions.
- Avoid introducing new decisions.
- Restrict changes strictly to documentation.

The Reviewer Agent MUST:

- Verify no normative decision exists exclusively in docs/architecture/.
- Verify all architecture docs contain a "Related ADRs" section.
- Verify no ADR has been weakened or altered.
- Confirm compliance with Definition of Done.

---

## 6. Validation

Validation MUST include manual review of:

- All files under docs/architecture/
- All files under docs/adr/

The Reviewer MUST confirm:

- No duplicated policy statements remain.
- No conflicting statements exist.
- Terminology is consistent across documents:
  - tenant_id
  - api_version
  - request_id
  - error.code
  - etc.

No automated tooling is required.

---

## 7. Definition of Done — STEP-01A

STEP-01A is complete only when ALL the following conditions are met.

### 7.1 Structural Alignment

- Every file in docs/architecture/ contains a "Related ADRs" section.
- All policy-level rules exist in ADRs.
- Architecture files reference ADRs instead of redefining decisions.

### 7.2 No Duplication

- No duplicated normative statements exist between:
  - docs/architecture/
  - docs/adr/

### 7.3 Governance Integrity

- No ADR content has been weakened.
- No decision has been silently removed.
- No new architectural decision has been introduced without ADR reference.

### 7.4 Scope Integrity

- No files outside docs/ were modified.
- No runtime behavior was changed.
- No configuration was altered.

---

## 8. Expected Outcome

After completing this STEP:

- docs/adr/ becomes the single authoritative source of architectural decisions.
- docs/architecture/ becomes the implementation guidance layer.
- Documentation maturity reaches enterprise-level clarity.
- Future STEPs can safely reference ADRs without ambiguity.
- Copilot agents operate with a clean governance separation.

This STEP concludes the architectural documentation consolidation phase.