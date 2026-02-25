Usa ARCHITECTURE.md, backend-structure.md, frontend-web.md, frontend-mobile.md, packages.md e gli ADR attuali.

Obiettivo: progettare il bootstrap iniziale del monorepo, senza ancora implementare logica business.

Voglio:

Struttura base di cartelle e progetti per:

backend/ (Django con backend_core e settings base/dev/prod)

frontend/web/ (React)

frontend/mobile/ (React Native, idealmente Expo)

packages/ per moduli riusabili backend

Elenco dei file iniziali da creare per ogni parte

Ordine suggerito dei passi (prima cosa fare, seconda, ecc.)

Evidenzia in che momenti bisogna stare attenti a multi-tenancy e security.

NON scrivere codice, solo piano dettagliato.