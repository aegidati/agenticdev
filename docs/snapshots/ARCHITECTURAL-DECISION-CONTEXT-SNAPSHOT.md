# ARCHITECTURAL DECISION CONTEXT SNAPSHOT

## Purpose

This file is a compact architectural memory snapshot.

It is designed to:

- Re-establish architectural context in future sessions.
- Prevent drift from accepted decisions.
- Provide continuity when resuming work.

It is not a replacement for full documentation.

---

# SYSTEM OVERVIEW

The system is a:

- Fullstack SaaS platform
- Multi-tenant
- Monorepo
- Backend: Django
- Web: React
- Mobile: React Native

Layered architecture:

- Domain
- Application
- Infrastructure
- Interfaces

Architecture precedes code.

---

# MULTI-TENANCY

Defined in ADR-001.

- Row-level isolation.
- All tenant-scoped tables include tenant_id.
- No global tenant state.
- No cross-tenant queries allowed.

Tenant isolation is security-critical.

---

# DATABASE

Defined in ADR-002.

- PostgreSQL primary engine.
- Repository abstraction required.
- DB is source of truth.
- Migrations version-controlled.

---

# AUTHENTICATION

Defined in ADR-003.

- JWT.
- RS256.
- kid header.
- Key rotation supported.
- Short-lived access tokens.
- Revocable refresh tokens.

---

# AUTHORIZATION

- RBAC.
- Tenant-scoped roles.
- Backend enforcement only.

---

# CACHING

Defined in ADR-004.

- Redis.
- Tenant-aware keys.
- TTL required.
- No sensitive data cached.

---

# RATE LIMITING

Defined in ADR-005.

- Redis-based.
- Per user.
- Per tenant.
- Per IP.

---

# ERROR HANDLING

Defined in ADR-015.

- Structured error format.
- No stack traces in production.
- Domain/Application/Infrastructure separation.

---

# OBSERVABILITY

Defined in ADR-019.

- Structured logs.
- tenant_id included.
- No secrets logged.

---

# TESTING

Defined in ADR-016.

- Test pyramid.
- Tenant isolation tests mandatory.
- Static checks mandatory.

---

# ARCHITECTURAL INVARIANTS

1. Tenant isolation mandatory.
2. No ORM in presentation layer.
3. No secrets in frontend.
4. DB is source of truth.
5. JWT must use RS256.
6. No cross-layer shortcuts.
7. Every structural change requires ADR.

---

# MATURITY STATUS

Foundational layer complete:

- Infrastructure baseline.
- Authentication skeleton.
- Multi-tenancy.
- Repository pattern.
- Testing foundation.

System ready for feature implementation.

---

To resume work:

Paste this file at start of new session and state:

"Continue architecture evolution from this snapshot."