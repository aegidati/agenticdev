Riprendiamo da questo snapshot. Proseguiamo con ADR-006.”

# ARCHITECTURAL DECISION CONTEXT SNAPSHOT  
## (Resume Context File for Future Chat Sessions)

---

## 1. Purpose

This file summarizes all architectural decisions and structural documentation defined so far.

It is designed to:

- Re-establish context in future ChatGPT sessions
- Provide a compact architectural memory snapshot
- Prevent drift from previously accepted decisions
- Ensure continuity when resuming work

This document is not a replacement for full documentation.  
It is a contextual summary to paste at the beginning of a new session.

---

# SYSTEM OVERVIEW

The system is a:

- Fullstack SaaS platform
- Multi-tenant
- Structured as a monorepo
- Backend: Python Django
- Web: React
- Mobile: React Native
- Shared backend modules in `packages/`

The architecture follows strict layered separation:

- Domain
- Application
- Infrastructure
- Interfaces (API / Presentation)

Architecture precedes code.

---

# MONOREPO STRUCTURE

High-level structure:

- backend/
- frontend/web/
- frontend/mobile/
- packages/
- docs/
  - architecture/
  - adr/

Packages are backend-only and UI-free.

Frontend layers are presentation-only.

---

# MULTI-TENANCY MODEL

Defined in:

- multi-tenancy.md
- ADR-001

Strategy:

- Row-level isolation
- All tenant-scoped tables include `tenant_id`
- Explicit Tenant Context required in repositories
- No global tenant state
- No cross-tenant queries allowed

Tenant isolation is a critical invariant.

---

# DATABASE STRATEGY

Defined in:

- database-abstraction.md
- ADR-002

Engine:

- PostgreSQL (primary production engine)

Design principles:

- Repository abstraction
- ORM-based (Django)
- Engine-agnostic design where possible
- Migrations version-controlled
- DB remains source of truth

---

# AUTHENTICATION STRATEGY

Defined in:

- authentication.md
- ADR-003

Strategy:

- JWT-based authentication
- RS256 signing (asymmetric)
- `kid` in header
- Key rotation supported
- Short-lived access tokens
- Refresh tokens revocable

Web:
- Access token in memory
- Refresh token in HTTP-only cookie

Mobile:
- Tokens stored in secure storage (Keychain / Keystore)

---

# AUTHORIZATION STRATEGY

Defined in:

- authorization.md

Model:

- Role-Based Access Control (RBAC)
- Tenant-scoped roles
- Backend enforces authorization
- Frontend only mirrors for UX

---

# CACHING STRATEGY

Defined in:

- ADR-004

Strategy:

- Redis as centralized cache
- Cache keys must include tenant_id when applicable
- Backend-centric caching
- DB remains source of truth
- No caching of sensitive data
- TTL must be defined

---

# RATE LIMITING STRATEGY

Defined in:

- ADR-005

Strategy:

- Redis-based centralized rate limiting
- Multi-level:
  - Per user
  - Per tenant
  - Per IP (for unauthenticated endpoints)
- Return HTTP 429
- Tenant-aware rate limit keys
- Observability required

---

# API VERSIONING

Defined in:

- api-versioning.md

Strategy:

- URL-based versioning (/api/v1/...)
- Breaking changes require major version bump
- Mobile compatibility must be preserved

---

# ERROR HANDLING

Defined in:

- error-handling.md

Model:

- Domain errors
- Application errors
- Infrastructure errors
- System errors

Standard error JSON format.

No stack traces exposed in production.

---

# LOGGING & OBSERVABILITY

Defined in:

- logging.md
- observability.md

Logging:

- Structured logs (JSON)
- Include request_id and tenant_id
- No secrets logged

Observability:

- Metrics (SLI/SLO)
- Tracing (future-ready)
- Alerting discipline
- Tenant-safe dashboards

---

# CI/CD STRATEGY

Defined in:

- ci-cd.md

Principles:

- Monorepo-aware pipeline
- Environment separation (dev/staging/prod)
- Security scanning
- Automated tests
- Version tagging
- Controlled production promotion

---

# PACKAGES LAYER

Defined in:

- packages.md

Rules:

- Backend-only
- No UI
- No circular dependencies
- Clear public APIs
- Independent testing

---

# FRONTEND WEB

Defined in:

- frontend-web.md

Principles:

- React
- Services layer for API calls
- No business logic in components
- Auth-aware routing
- Tenant context in global state
- No secrets in frontend

---

# FRONTEND MOBILE

Defined in:

- frontend-mobile.md

Principles:

- React Native
- Secure token storage
- OAuth + PKCE for social login
- Tenant-scoped state
- Offline-aware design
- No secrets in bundle

---

# SECURITY MODEL

Defined in:

- security-model.md

Principles:

- Input validation
- Secret management
- No token logging
- Layer isolation
- Tenant isolation is security-critical

---

# ACTIVE ADR LIST

- ADR-001 — Multi-Tenancy Isolation Strategy
- ADR-002 — Database Engine Strategy
- ADR-003 — JWT Signing & Key Rotation Strategy
- ADR-004 — Caching Strategy
- ADR-005 — API Rate Limiting Strategy

---

# ARCHITECTURAL INVARIANTS (MUST NEVER BE VIOLATED)

1. Tenant isolation is mandatory.
2. Domain logic must not leak into presentation layer.
3. DB is source of truth.
4. No secrets in frontend.
5. JWT must use RS256.
6. Cache keys must be tenant-aware.
7. Rate limiting must be centralized.
8. API versioning must be explicit.
9. No cross-layer shortcuts.
10. Any structural change requires new ADR.

---

# HOW TO USE THIS FILE IN A NEW CHAT

At the start of a future session:

1. Paste this entire file.
2. State:
   "Continue the architecture evolution from this snapshot."
3. Then specify what to work on:
   - New ADR
   - New Feature
   - Refactoring
   - Performance strategy
   - Scaling strategy
   - Compliance extension

This ensures continuity without re-explaining the full system.

---

# CURRENT ARCHITECTURE MATURITY LEVEL

The system currently has:

- Layered architecture discipline
- Multi-tenant enforcement
- Secure JWT strategy
- Redis-based caching
- Centralized rate limiting
- Observability model
- CI/CD governance
- Formal ADR process

The architecture is enterprise-ready at foundational level.

Further evolution should focus on:

- Background jobs
- Feature flags
- Horizontal scaling
- Audit logging
- Compliance
- Data partitioning



