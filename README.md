🧱 Superstack Architecture Rulebook

Deterministic · Zero-Trust · DB-First · Production-Ready

This repository documents an opinionated, real-world architecture standard for building modern web + AI systems without vendor lock-in, hidden runtimes, or abstraction debt.

It is not a framework.
It is not a starter kit.
It is a systems rulebook.

If you’ve ever asked:
	•	“Why does this platform feel magical until prod?”
	•	“Where exactly does my data live?”
	•	“Why does scaling break everything?”

This repo is the answer I wish existed earlier.

⸻

What This Is

A Convex-class open architecture specification built from:
	•	First-principles systems design
	•	Database-first thinking
	•	Zero-trust networking
	•	Deterministic builds and deployments
	•	Real production failure modes

It reflects how senior engineers actually ship and operate systems, not how platforms market themselves.

⸻

What This Is Not
	•	❌ A tutorial
	•	❌ A “10x dev” productivity hack
	•	❌ A replacement for thinking
	•	❌ A proprietary platform

This assumes you are comfortable with:
	•	Linux
	•	Containers
	•	Databases
	•	Networking
	•	Reading documentation

⸻

Core Principles
	•	Determinism over convenience
	•	Databases are the source of truth
	•	Compute moves toward data
	•	Zero-trust by default
	•	Minimize abstractions
	•	Design for failure, not demos
	•	Own your stack end-to-end

⸻

Repository Structure

.
├── README.md                  # This file

	├── RULEBOOK.md                # Non-negotiable architectural rules

		├── PODMAN-COMPOSE_REF.md      # Production Podman Compose reference

			├── HEALTHCHECK.md             # Healthcheck & postmortem standards

				├── CC-OAS.md                  # Convex-Class Open Architecture Spec

└── LinkedIn.md                # Public-facing narrative & positioning

Each file is self-contained, explicit, and written to be read independently.

⸻

File Overview

📘 RULEBOOK.md

The operating doctrine.

Defines:
	•	Network isolation rules
	•	Security boundaries
	•	Data ownership principles
	•	Tooling constraints
	•	What is allowed vs forbidden

If you only read one file — read this.

⸻

🧩 PODMAN-COMPOSE_REF.md

A production-first Podman Compose reference implementing the rulebook.

Includes:
	•	Triple network isolation
	•	Service placement
	•	Secrets handling
	•	Healthchecks
	•	Deterministic container usage

This is how the rules turn into infrastructure.

⸻

❤️ HEALTHCHECK.md

Standards for:
	•	Liveness checks
	•	Readiness checks
	•	Dependency awareness
	•	Blameless postmortems
	•	Incident severity classification

This file exists because most outages are operational, not technical.

⸻

⚙️ CC-OAS.md

Convex-Class Open Architecture Specification

A formal architecture spec describing:
	•	How to achieve Convex-level DX
	•	Without proprietary runtimes
	•	Without opaque data ownership
	•	With explicit systems boundaries

Written like an internal RFC, not marketing copy.

⸻

🧠 LinkedIn.md

A concise public narrative explaining:
	•	Why this architecture exists
	•	What problem it solves
	•	How to talk about it without sounding insane online

Optional — but useful.

⸻

Who This Is For

This repo is for:
	•	Senior SWE / DevOps / Platform engineers
	•	AI engineers who care about data gravity
	•	Founders who want to own their infrastructure
	•	Teams burned by “backend as a service” abstractions
	•	Anyone transitioning from tool user → systems thinker

⸻

How To Use This Repo
	•	Use it as a reference, not a checklist
	•	Copy patterns, not blindly configs
	•	Adapt it to your constraints
	•	Argue with it — that’s the point

If it forces you to think more clearly about your system, it’s working.

⸻

Final Note

Good systems feel boring.
Bad systems feel magical — until they fail.

This repository exists to make systems legible, auditable, and operable from day one.

No hype.
No magic.
Just architecture.
