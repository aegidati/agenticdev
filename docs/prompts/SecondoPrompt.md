Prendi il piano generato dal Planner (incolla o riferisci il messaggio) e implementa: Step 1 — Monorepo root scaffold

Create: backend, frontend, frontend/web, frontend/mobile, packages
Create: .github/workflows
Create: root bootstrap docs: README.md, .gitignore, .editorconfig
Attention point (security): define secret-handling policy before any env files.
Step 2 — Backend project shell (Django core first)

Create: backend/manage.py
Create: backend/backend_core
Create: backend/backend_core/settings/base.py
Create: backend/backend_core/settings/dev.py
Create: backend/backend_core/settings/prod.py
Create: backend/backend_core/urls.py, backend/backend_core/asgi.py, backend/backend_core/wsgi.py
Attention point (security): fail-fast config validation and no insecure defaults in base settings.