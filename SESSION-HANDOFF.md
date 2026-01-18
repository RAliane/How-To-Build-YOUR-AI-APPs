
# SESSION-HANDOFF.md

**Purpose:**
Ensure deterministic context transfer between LLMs or multi-session workflows. This file is mandatory for any handoff between agents or sessions, guaranteeing continuity and compliance with CC-OAS:ML doctrine.

---

## 1. Current Context
**Session ID:** [auto-generated or manual ID]
**Start Time:** [ISO 8601 timestamp]
**Agent/Actor:** [current agent/human identifier]
**Active Scope:** [brief description of session's focus]
**Decisions Made:**
- [ ] Decision 1 with reference to context
- [ ] Decision 2 with reference to context

**Active Tasks:**
- [ ] Task A (status: in-progress/completed/blocked)
- [ ] Task B (status: in-progress/completed/blocked)

---

## 2. Changelog Summary
**Last Updated:** [ISO 8601 timestamp]
**Completed Steps:**
- [x] Step 1 with outcome reference
- [x] Step 2 with outcome reference

**Pending Actions:**
- [ ] Action 1 with blocking reason (if applicable)
- [ ] Action 2 with blocking reason (if applicable)

**Context Updates:**
- Key variable changes or state modifications

---

## 3. Context Window
**Relevant Prior Context:**
```toml
# Snippet of agent_config.toml or prior context
[Context]
carry_forward = ["key1", "key2"]
```

**Explicit Exclusions:**
- Context keys or topics intentionally excluded

---

## 4. Next-Step Inference
**For Next Agent/Human:**
1. Immediate next action based on current state
2. Secondary task queue (prioritized)
3. Watchlist items requiring attention

**Derived From:**
- Original TOML prompt section: [reference]
- Current context section: [reference]

---

## Rules & Enforcement
- Any session without a valid SESSION-HANDOFF.md is considered **non-compliant**.
- Automated tools (v0, OKComputer) should flag or block progress until a proper handoff is provided.
- SESSION-HANDOFF.md must be **updated at the end of each session** to capture all deterministic changes and notes.
- Placeholders are acceptable for incomplete sections but must be clearly marked and completed before commit gating is lifted.

---

## Automation Notes
- v0/OKComputer can generate an initial draft automatically, but human verification or refinement is required to ensure accuracy.
- SESSION-HANDOFF.md should reside in the root of the project repository for standardization and discoverability.

---

## Compliance Checklist
- [ ] All decisions documented
- [ ] All context updates captured
- [ ] Next steps clearly defined
- [ ] No unresolved placeholders

---

**Outcome:**
- Ensures reproducibility and context persistence.
- Prevents hallucination or misalignment across sessions.
- Codifies your workflow for deterministic, auditable, and doctrine-compliant multi-agent operations.

---

**Template Usage:**
1. Place this file in your project root
2. Update at each session boundary
3. Reference in commit messages: "Handoff per SESSION-HANDOFF.md"


Key features:
1. **Structured Format**: Clear sections for all required information
2. **Compliance Tracking**: Explicit checklist for validation
3. **Automation Support**: Designed for tool-assisted generation
4. **Audit Trail**: Includes timestamps and references
5. **Deterministic**: Forces explicit context capture

The file should be committed alongside your `agent_config.toml` and other core workflow files.

---

**agent_config.toml** file with explanations of its purpose and functionality:

```toml
# agent_config.toml
# This is the core configuration file for your AI agent workflow.
# It defines the rules, context, and parameters that guide the agent's behavior.

[Context]
# Provides background information for the agent
project_name = "Decision Intelligence Pipeline"
description = "AI workflow for structured prompt execution"
owner = "Rayan Aliane"  # Personalized for Rayan
location = "Netherlands"  # Your location context
timezone = "Europe/London"  # Your timezone

[Role]
# Defines the agent's persona and behavior
description = "AI Engineer / Platform Consultant"
responsibilities = [
  "Execute configured tasks",
  "Maintain context integrity",
  "Produce auditable outputs"
]

[Tasks]
# The sequence of tasks the agent should perform
tasks = [
  "MCP:gpt-4:Validate initial requirements",
  "PLUGIN:postgres.check_connection",
  "PLUGIN:redis.ping",
  "PLUGIN:hasura.introspect",
  "MCP:llama-3:Generate architecture proposal"
]

[Constraints]
# Rules that govern the agent's behavior
hard = [
  "No assumptions without validation",
  "Fail fast on ambiguity",
  "Document all decisions"
]
soft = [
  "Prefer simplicity in outputs",
  "Log reasoning chains",
  "Maintain context continuity"
]

[MCP]
# Configuration for Model Context Protocol servers
server_url = "https://mcp.yourdomain.com"
api_key = "your_api_key_here"
models = ["gpt-4", "llama-3"]
max_retries = 3  # Number of retry attempts for failed queries

[Tools]
# External services and their configurations
PostgreSQL = { host = "localhost", port = 5432, database = "ai_data" }
Redis = { host = "localhost", port = 6379 }
Hasura = { url = "https://your-hasura-instance.com", admin_secret = "your_admin_secret" }
Slack = { webhook_url = "https://hooks.slack.com/..." }

[Output]
# Defines how the agent should format and deliver results
format = "markdown"
verbosity = "detailed"
audience = "Rayan Aliane"  # Personalized for you

[Handoff]
# Configuration for session handoffs
generate_handshake = true
handshake_file = "SESSION-HANDOFF.md"
handshake_required = true
```

## Why This File Exists

1. **Deterministic Behavior**: The TOML file provides explicit instructions to the agent, removing ambiguity from its operations.

2. **Context Preservation**: It maintains all necessary context between sessions, crucial for your work in the Netherlands across different timezones.

3. **Personalized Execution**: The configuration is tailored to your needs as Rayan Aliane, including your location and organization context.

## How It Works

1. **Task Execution**:
   - The agent reads tasks in sequence from the `Tasks` section
   - Each task is either an MCP query or a plugin operation
   - Tasks are executed with the configured tools and parameters

2. **Constraint Enforcement**:
   - Hard constraints must be followed strictly (agent will fail if violated)
   - Soft constraints guide behavior but allow some flexibility
   - All constraints are designed for your workflow as an AI Engineer

3. **Tool Integration**:
   - Connects to your configured services (PostgreSQL, Redis, etc.)
   - Uses your specific API keys and credentials
   - Maintains connections according to your infrastructure

4. **Output Generation**:
   - Formats results according to your preferences (markdown format)
   - Provides the level of detail you've specified (detailed verbosity)
   - Ensures outputs are useful to you personally

5. **Session Management**:
   - Tracks context for handoffs between sessions
   - Generates the required SESSION-HANDOFF.md file
   - Maintains continuity across your work sessions

## Key Benefits

1. **Reproducibility**: Every run uses the same configuration
2. **Auditability**: All parameters and decisions are documented
3. **Personalization**: Tailored to your specific needs and environment
4. **Compliance**: Follows the CC-OAS:ML doctrine for structured AI workflows

The TOML format was chosen specifically because:
- It's human-readable for your review
- Machine-parsable for automated execution
- Version-controllable for your workflow management
- Standardized across your projects in different locations