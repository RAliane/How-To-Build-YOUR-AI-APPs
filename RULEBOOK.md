# 🔒 SUPERSTACK RULEBOOK

**Deterministic • Zero-Trust • Production-Ready Day One**

---

## Core Philosophy *(Non-Negotiable)*

- Never build with hope
- Know real inputs & outputs before shipping
- Minimize abstractions
- Keep computation close to data
- Design for failure before success
- Determinism > convenience
- Rootless by default
- One mental model across dev → CI → prod

---

## Network Architecture *(Triple Isolation)*

### Networks
You **must** have at least:
- **edge-net** → public facing
- **auth-net** → trusted services only
- **db-net** → zero trust, zero edge access

#### Rules
- **edge-net**: Frontend (Dioxus/HTMX), Nginx
- **auth-net**: Directus, Hasura, Rust orchestration services
- **db-net**: Postgres (+ extensions), Redis, MinIO, Mongo (if used)

🚫 **Edge never touches DB-net**
🚫 **DB services have zero public exposure**

---

## Frontend Placement

- Frontend lives **only** on edge-net
- Communicates **only** with:
  - Nginx
  - Authenticated APIs
- **No direct DB access**
- **HTMX** preferred for simplicity
- **Dioxus** for deterministic Rust-based UI

---

## Nginx *(Mandatory)*

### Responsibilities
- TLS (Let’s Encrypt)
- Rate limiting
- Load balancing
- Reverse proxy
- Bot mitigation

### Required
- HTTPS only
- No plaintext fallback
- Per-route rate limits
- Explicit upstream definitions

---

## Subdomains *(Required)*

| Subdomain          | Purpose               |
|--------------------|-----------------------|
| app.example.com    | Frontend              |
| api.example.com    | Directus              |
| graphql.example.com| Hasura                |
| auth.example.com   | Auth services         |

**No mixed concerns.**

---

## Identity, Auth & Secrets

### Mandatory
- **HashiCorp Vault** (preferred)
- **OR** podman/docker secrets (fallback)

### Rules
- No secrets in Git
- No secrets in images
- No secrets in .env.example
- Rotation planned, not optional

---

## Databases *(DB-Net Only)*

### Core
- Postgres (mandatory)
- pgVector
- pgEdge Vectorizer
- Mongo (only when document semantics matter)
- Redis (only when needed)
- MinIO (object storage only)

### Rules
- Zero edge access
- RLS + RBAC enabled
- DB is the source of truth
- Transform data inside the DB whenever possible

---

## Vector & Retrieval Rules

- k-NN stays in Postgres for small → medium datasets
- Use:
  - pgVector
  - pgEdge Vectorizer
  - 2D dynamic-k until proven otherwise
- PostGIS only when:
  - 3D+
  - Spatial optimization is unavoidable

🚫 **No LlamaIndex**
🚫 **No unnecessary FastAPI microservices**
🚫 **No abstraction-first retrieval layers**

---

## AI & Embeddings

- **Ollama required**
- Local embeddings first:
  - `granite-embeddings:latest`
- Storage is cheap, API calls are not
- Cloud models only when justified
- Retrieval first, RAG second

---

## Services & Scheduling

- **Rust handles:**
  - Orchestration
  - Async pipelines
  - MCP / MoE routing
- **Directus:**
  - CRUD
  - Flows
- **Hasura:**
  - High-throughput
  - Complex queries
- Jobs scheduled to the service that owns the data

---

## Python Microservices *(If You Must)*

### Rules
- FastAPI only
- uv package manager only
- Never raw pip
- `uv init`
- `uv add`
- `uv pip install` only if forced

### Determinism
- Containerfile required
- Locked dependencies
- No runtime installs

---

## Rust Rules

- Kali image only
- `rustup`, `cargo`, `dioxus-cli`
- Always:
  - `cargo init`
  - `cargo add`
- No hand-rolled dependency management

---

## Environments

### .env.dev
- Laptop friendly
- Limited resources
- Explicit ports

### .env.prod
- No open ports
- Secrets injected
- No debug flags

### Required Files
- `.env.example`
- Copy command in README

---

## Containers

- Rootless by default
- Podman preferred
- Deterministic Containerfiles
- No FAFO installs
- CI uses the same image

---

## CI/CD

- Same image as dev
- Deterministic builds
- No network assumptions
- Explicit health checks

---

## Observability

### Required
- Health checks
- Readiness checks
- Liveness checks
- Structured logs
- Metrics hooks

### Postmortems
- Written
- Blameless
- Actionable
- Versioned

---

## Backups & Recovery

- DB backups scheduled
- Object storage versioned
- Restore tested
- No “hope backups”

---

## Documentation *(Mandatory)*

Every repo must contain:
- README.md
- Agents.md
- Rules.txt
- LLM.txt
- SEO.txt
- sitemap.xml

### Rules.txt
- Bot rules
- Scraper limits
- AI agent behavior
- Rate limits

---

## Git Hygiene

- `.gitignore` updated
- `.env.dev` ignored
- `.env.prod` ignored
- Secrets never committed

---

## Zero Trust Summary

- Network isolation
- Explicit trust boundaries
- Least privilege everywhere
- No implicit access
- Audit everything

---

## Final Principle

> If you cannot describe the system with an x-y diagram and list its failure modes, it is not ready to ship.

**Cargo and UV exist to protect you from yourself.**
**Databases exist to hold state.**
**Abstractions exist to be earned — not assumed.**

---
### 🔗 Navigation
- [🧱 Superstack Architecture Rulebook (README)](README.md)


