
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