🔒 SUPERSTACK RULEBOOK

Deterministic • Zero-Trust • Production-Ready Day One

⸻

0. Core Philosophy (Non-Negotiable)
	•	Never build with hope
	•	Know real inputs & outputs before shipping
	•	Minimize abstractions
	•	Keep computation close to data
	•	Design for failure before success
	•	Determinism > convenience
	•	Rootless by default
	•	One mental model across dev → CI → prod

⸻

1. Network Architecture (Triple Isolation)

Networks

You must have at least:

edge-net     → public facing
auth-net     → trusted services only
db-net       → zero trust, zero edge access

Rules
	•	edge-net
	•	Frontend (Dioxus / HTMX)
	•	Nginx
	•	auth-net
	•	Directus
	•	Hasura
	•	Rust orchestration services
	•	db-net
	•	Postgres (+ extensions)
	•	Redis
	•	MinIO
	•	Mongo (if used)

🚫 Edge never touches DB-net
🚫 DB services have zero public exposure

⸻

2. Frontend Placement
	•	Frontend lives only on edge-net
	•	Communicates only with:
	•	Nginx
	•	Authenticated APIs
	•	No direct DB access
	•	HTMX preferred for simplicity
	•	Dioxus for deterministic Rust-based UI

⸻

3. Nginx (Mandatory)

Responsibilities
	•	TLS (Let’s Encrypt)
	•	Rate limiting
	•	Load balancing
	•	Reverse proxy
	•	Bot mitigation

Required
	•	HTTPS only
	•	No plaintext fallback
	•	Per-route rate limits
	•	Explicit upstream definitions

⸻

4. Subdomains (Required)

Example:

app.example.com        → frontend
api.example.com        → Directus
graphql.example.com    → Hasura
auth.example.com       → auth services

No mixed concerns.

⸻

5. Identity, Auth & Secrets

Mandatory
	•	HashiCorp Vault (preferred)
	•	OR podman/docker secrets (fallback)

Rules
	•	No secrets in Git
	•	No secrets in images
	•	No secrets in .env.example
	•	Rotation planned, not optional

⸻

6. Databases (DB-Net Only)

Core
	•	Postgres (mandatory)
	•	pgVector
	•	pgEdge Vectorizer
	•	Mongo (only when document semantics matter)
	•	Redis (only when needed)
	•	MinIO (object storage only)

Rules
	•	Zero edge access
	•	RLS + RBAC enabled
	•	DB is the source of truth
	•	Transform data inside the DB whenever possible

⸻

7. Vector & Retrieval Rules
	•	k-NN stays in Postgres for small → medium datasets
	•	Use:
	•	pgVector
	•	pgEdge Vectorizer
	•	2D dynamic-k until proven otherwise
	•	PostGIS only when:
	•	3D+
	•	spatial optimization is unavoidable

🚫 No LlamaIndex
🚫 No unnecessary FastAPI microservices
🚫 No abstraction-first retrieval layers

⸻

8. AI & Embeddings
	•	Ollama required
	•	Local embeddings first:
	•	granite-embeddings:latest
	•	Storage is cheap
	•	API calls are not
	•	Cloud models only when justified
	•	Retrieval first, RAG second

⸻

9. Services & Scheduling
	•	Rust handles:
	•	orchestration
	•	async pipelines
	•	MCP / MoE routing
	•	Directus:
	•	CRUD
	•	flows
	•	Hasura:
	•	high-throughput
	•	complex queries
	•	Jobs scheduled to the service that owns the data

⸻

10. Python Microservices (If You Must)

Rules
	•	FastAPI only
	•	uv package manager only
	•	Never raw pip
	•	uv init
	•	uv add
	•	uv pip install only if forced

Determinism
	•	Containerfile required
	•	Locked dependencies
	•	No runtime installs

⸻

11. Rust Rules
	•	Kali image only
	•	rustup, cargo, dioxus-cli
	•	Always:
	•	cargo init
	•	cargo add
	•	No hand-rolled dependency management

⸻

12. Environments

.env.dev
	•	Laptop friendly
	•	Limited resources
	•	Explicit ports

.env.prod
	•	No open ports
	•	Secrets injected
	•	No debug flags

Required Files
	•	.env.example
	•	Copy command in README

⸻

13. Containers
	•	Rootless by default
	•	Podman preferred
	•	Deterministic Containerfiles
	•	No FAFO installs
	•	CI uses the same image

⸻

14. CI/CD
	•	Same image as dev
	•	Deterministic builds
	•	No network assumptions
	•	Explicit health checks

⸻

15. Observability

Required
	•	Health checks
	•	Readiness checks
	•	Liveness checks
	•	Structured logs
	•	Metrics hooks

Postmortems
	•	Written
	•	Blameless
	•	Actionable
	•	Versioned

⸻

16. Backups & Recovery
	•	DB backups scheduled
	•	Object storage versioned
	•	Restore tested
	•	No “hope backups”

⸻

17. Documentation (Mandatory)

Every repo must contain:

README.md
Agents.md
Rules.txt
LLM.txt
SEO.txt
sitemap.xml

Rules.txt
	•	Bot rules
	•	Scraper limits
	•	AI agent behavior
	•	Rate limits

⸻

18. Git Hygiene
	•	.gitignore updated
	•	.env.dev ignored
	•	.env.prod ignored
	•	Secrets never committed

⸻

19. Zero Trust Summary
	•	Network isolation
	•	Explicit trust boundaries
	•	Least privilege everywhere
	•	No implicit access
	•	Audit everything

⸻

20. Final Principle

If you cannot describe the system with an x-y diagram and list its failure modes, it is not ready to ship.

Cargo and UV exist to protect you from yourself.
Databases exist to hold state.
Abstractions exist to be earned — not assumed.

