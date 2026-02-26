# STEP 01 — Monorepo Bootstrap (Governed Copilot Execution Prompt)

## Copilot Mode

Use: **Agent Mode**

Run this prompt from the root of the repository in VS Code.

---

## Objective

Create the initial monorepo structure and bootstrap a Django backend project, strictly aligned with the defined ADRs and the Prompt Governance Convention.

This step establishes structural foundations only.

No business logic.
No infrastructure configuration.
No authentication.
No background jobs.

Architecture before implementation.

---

## Mandatory ADR Compliance

You MUST comply with:

- ADR-001 — Multi-Tenancy Isolation Strategy
- ADR-002 — Database Engine Strategy
- ADR-009 — Horizontal Scaling & Load Balancing Strategy

You MUST NOT violate:

- ADR-006 — Background Job Processing Strategy
- ADR-011 — Event-Driven Architecture Strategy
- ADR-012 — Distributed Tracing Strategy
- ADR-014 — Advanced Secret Management Strategy

You must assume that `PROMPT-GOVERNANCE-CONVENTION.md` exists and governs this execution.

---

## Architectural Constraints

You MUST enforce the following structural rules:

### 1. Layer Separation

Under `backend/`, create the following folders:

- domain/
- application/
- infrastructure/
- interfaces/
- settings/

Rules:

- `domain/` MUST NOT import Django, ORM, infrastructure, or interfaces.
- `infrastructure/` MAY depend on domain.
- `interfaces/` MUST NOT contain business logic.
- `application/` will orchestrate domain + infrastructure.
- No circular dependencies.

---

### 2. Stateless Web Discipline (ADR-009)

- Do NOT introduce session-based logic.
- Do NOT configure in-memory storage.
- No assumptions about sticky sessions.

---

### 3. Tenant Awareness (ADR-001)

- Do NOT implement tenant logic yet.
- Structure must allow tenant-aware repositories later.
- No global mutable state.

---

### 4. Secrets (ADR-014)

- Do NOT create `.env`.
- Do NOT add credentials.
- Do NOT embed secrets in settings.
- Use Django default SQLite config for now (temporary and acceptable for bootstrap).

---

### 5. No Business Logic

- Only placeholder modules.
- Only structure.
- Only minimal Django bootstrapping.

---

## Tasks

### Step 1 — Create Backend Folder

If not existing:

- Create `backend/`.

---

### Step 2 — Initialize Django Project

Inside `backend/`:

- Initialize a Django project (e.g. project name: `core`).
- Ensure:
  - `backend/manage.py` exists.
  - `backend/core/` exists.

Do NOT create Django apps yet.

---

### Step 3 — Create Layered Structure

Inside `backend/`, create:

- domain/
- application/
- infrastructure/
- interfaces/
- settings/

Each must contain:

- `__init__.py`

---

### Step 4 — Create Placeholder Modules

Create the following files:

#### backend/domain/events.py

- Define a minimal `DomainEvent` base class.
- It must NOT import Django.
- Use a simple Python class or dataclass.
- Add docstring referencing ADR-011.

---

#### backend/application/services.py

- Add explanatory docstring:
  - This layer orchestrates use cases.
  - It coordinates domain + infrastructure.
  - It is ADR-001 compliant (tenant-aware).

No implementation logic.

---

#### backend/infrastructure/repositories.py

- Add explanatory docstring:
  - This module will implement ORM-backed repositories.
  - Must enforce tenant isolation (ADR-001).
  - Must comply with ADR-002.

No implementation logic.

---

#### backend/interfaces/api.py

- Add explanatory docstring:
  - This module will expose REST endpoints.
  - No business logic allowed.
  - Must remain stateless (ADR-009).

Do NOT implement actual endpoints.

---

### Step 5 — Settings Restructuring

Under `backend/settings/`, create:

- __init__.py
- base.py

Move minimal Django settings into `settings/base.py`.

Modify the main Django settings loader to import from `settings.base`.

Ensure:

- Project still runs.
- No secrets introduced.
- SQLite default DB acceptable for bootstrap only.

---

### Step 6 — Validation

Ensure:

- `python backend/manage.py check` runs without errors.
- No import errors between layers.
- Django server can start.

---

## Non-Goals (Hard Constraints)

You MUST NOT:

- Create Django models.
- Configure Celery.
- Add Redis.
- Add JWT.
- Add REST Framework.
- Add Feature Flags.
- Add Event Bus.
- Add Outbox pattern.
- Add tracing middleware.
- Add third-party packages beyond Django default.

---

## Expected Repository Structure

After execution, repository should resemble:

root/
│
├── backend/
│   ├── manage.py
│   ├── core/
│   ├── domain/
│   ├── application/
│   ├── infrastructure/
│   ├── interfaces/
│   └── settings/
│
├── frontend/
│   ├── web/
│   └── mobile/
│
├── packages/
│
└── docs/

---

## Post-Execution Report (Mandatory)

After proposing changes, you MUST:

1. List all created files.
2. List modified files.
3. Confirm explicitly:

   - Domain layer does NOT import Django.
   - No circular dependencies.
   - No secrets introduced.
   - Architecture remains ADR-compliant.

4. Suggest manual verification steps:

   - Run `python backend/manage.py check`
   - Run `python backend/manage.py runserver`
   - Inspect imports between layers.

If any suggestion violates ADR or governance rules,
you MUST correct it before finalizing.

---

## Final Reminder

Architecture > Prompt > Code.

You are not just generating code.
You are implementing an architectural foundation.