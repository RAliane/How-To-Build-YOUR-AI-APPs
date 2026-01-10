⚙️ Convex-Class Open Architecture Specification (CC-OAS)

Status: Draft v1
Audience: Senior SWE, DevOps, Platform, AI Engineers
Goal: Define a deterministic, open alternative to Convex-style platforms

---

1. Problem Statement

Modern “backend platforms” (Convex, Firebase, Supabase-style abstractions):
	-	Hide databases behind proprietary APIs
	-	Centralize logic in opaque runtimes
	-	Trade determinism for developer convenience
	-	Collapse trust boundaries
	-	Become impossible to reason about at scale

CC-OAS defines a system that delivers:
	-	Convex-level developer velocity
	-	Without proprietary lock-in
	-	Without hidden compute
	-	With explicit data ownership
	-	With production-grade security on day one

---

2. Design Goals (Hard Requirements)

G1 — Determinism
	-	Every input → output path is traceable
	-	No hidden side effects
	-	No magical runtime behavior

G2 — DB-First
	-	Database is the source of truth
	-	Business logic moves toward data, not away from it
	-	No “backend SDK owns your data”

G3 — Zero-Trust by Default
	-	Network isolation
	-	Explicit service boundaries
	-	Least privilege everywhere

G4 — Convex-Class DX
	-	Real-time capable
	-	Reactive data
	-	Simple CRUD
	-	Fast iteration

G5 — Open & Replaceable
	-	Every component is swappable
	-	No single vendor dependency
	-	No proprietary protocol requirements

---

3. Core Architectural Layers
```
┌──────────────────────────────┐
│          Frontend            │
│   (HTMX / Dioxus / Web)      │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│         Edge Layer           │
│   (Nginx, TLS, Rate Limit)   │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│     Application Control      │
│ (Directus + Hasura + Rust)   │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│        Data Plane            │
│ (Postgres, Redis, MinIO)     │
└──────────────────────────────┘
```
Each layer is explicit, isolated, and replaceable.

---

4. Data Plane Specification (The Core)

Mandatory Components

Postgres
	-	Single source of truth
	-	RLS + RBAC enabled
	-	Extensions allowed:
	-	pgvector
	-	pg_edge_vectorizer
	-	postgis (only when justified)

Redis (Optional)
	-	Ephemeral state
	-	Locks
	-	Queues
	-	Never authoritative

MinIO (Optional)
	-	Object storage
	-	Static assets
	-	Backups

📌 Rule:
If logic can be expressed in SQL safely, it belongs in the DB.

---

5. Application Control Layer

Directus (Primary Control Plane)
	-	CRUD
	-	Admin UI
	-	Schema governance
	-	Flows for orchestration

Acts as the “Convex mutation layer”, but transparently over Postgres.

---

Hasura (High-Throughput Query Plane)
	-	GraphQL over Postgres
	-	Subscription support
	-	Fine-grained permissions
	-	Optimized read paths

Acts as the “Convex query engine”, without owning your data.

---

Rust Services (Execution Plane)
	-	Async orchestration
	-	AI pipelines
	-	MCP servers
	-	Deterministic background work

Acts as the “Convex function runtime”, but explicit and inspectable.

---

6. Real-Time & Reactivity Model

Instead of a proprietary real-time engine:
	-	Postgres NOTIFY / LISTEN
	-	Hasura subscriptions
	-	Directus events
	-	Redis pub/sub (optional)

📌 Reactivity emerges from data change, not runtime magic.

---

7. AI / Vector / RAG Specification

Embeddings
	-	Generated locally via Ollama
	-	Stored in Postgres (pgvector)
	-	Indexed in-DB

Retrieval
	-	k-NN in SQL
	-	Dynamic-k
	-	No external retrieval engines for small/medium scale

Generation
	-	Optional
	-	Happens after retrieval
	-	Never conflated with storage

📌 This mirrors Convex’s “compute near data” philosophy — but open.

---

8. Security Model

Network Isolation
	-	Edge-Net
	-	Auth-Net
	-	DB-Net

Identity
	-	Vault-managed secrets
	-	No inline secrets
	-	No public DB access

Access Control
	-	Postgres RLS
	-	Hasura permissions
	-	Directus RBAC

📌 Security is structural, not policy-based.

---

9. Deployment & Operations

Containers
	-	Rootless
	-	Deterministic
	-	Same image for dev / CI / prod

Healthchecks
	-	Liveness
	-	Readiness
	-	Dependency-aware

Postmortems
	-	Mandatory
	-	Blameless
	-	Action-driven

📌 Operational discipline is part of the spec.

---

10. What Makes This “Convex-Class”

Convex Feature	CC-OAS Equivalent
Reactive data	DB-driven reactivity
Server functions	Rust services
Transactions	Postgres
Auth rules	RLS + RBAC
Real-time	Subscriptions
DX	Opinionated defaults

But:
	-	No vendor lock-in
	-	No opaque runtime
	-	No proprietary protocol

---

11. Explicit Non-Goals
	-	No magic global state
	-	No hidden compute billing
	-	No “just trust the platform”
	-	No closed source runtime
	-	No replacing SQL with abstractions

---

12. Summary (The Thesis)

Convex solved developer experience by hiding systems.
CC-OAS solves developer experience by making systems legible.

This architecture assumes:
	-	You want to own your data
	-	You want to reason about failure
	-	You want Convex-level speed without Convex-level opacity

