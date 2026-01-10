LinkedIn_Posting_RuleBook_v3.1.md
single-file, agent-readable, CI/CD pipeline inside
Rayan Aliane – 2026-01-09
NAV
00-Philosophy | 01-Principles | 02-Outcome-Picker | 03-Hook-Menu | 04-Depth-Gradient | 05-Skeleton | 06-Invitation | 07-Voice | 08-Timing | 09-Hashtags | 10-Evergreen | 11-KillList | 12-Templates | 12b-Pipeline | 13-Swipe-File | 14-Metrics | 15-Post-Mortem | 16-Final-Gate | 17-Boring-Test | 18-Versioning | 19-Changelog
----
00-Philosophy
Signal  >  Noise
Builders >  Broad appeal
Systems  >  Hot takes# LinkedIn_Posting_RuleBook_v3.1.md
# Single-file, agent-readable, CI/CD pipeline inside
# Rayan Aliane – 2026-01-09

---

## NAV
00-Philosophy | 01-Principles | 02-Outcome-Picker | 03-Hook-Menu | 04-Depth-Gradient | 05-Skeleton | 06-Invitation | 07-Voice | 08-Timing | 09-Hashtags | 10-Evergreen | 11-KillList | 12-Templates | 12b-Pipeline | 13-Swipe-File | 14-Metrics | 15-Post-Mortem | 16-Final-Gate | 17-Boring-Test | 18-Versioning | 19-Changelog

---

## 00-Philosophy
- Signal > Noise
- Builders > Broad appeal
- Systems > Hot takes
- Compounding > Virality

---

## 01-Principles
- One outcome per post (pick before you write).
- Clarity + brevity; whitespace is free.
- Every technical claim carries a constraint or failure mode.
- If it isn’t boring enough to run in prod, it isn’t ready.

---

## 02-Outcome-Picker *(choose one)*
- Authority
- Network
- Relationship
- Opportunity
- Idea-test

> **No outcome → no post.**

---

## 03-Hook-Menu *(first 2 lines)*
- Contrarian
- Failure-first
- Comparison
- Reduction
- Temporal
- Pattern-reveal

> **No hook → rewrite.**

---

## 04-Depth-Gradient *(never start at 3)*
1. Why it matters
2. How it works (concept)
3. Implementation
4. Where it breaks

> **Include one translation sentence for L3-4.**

---

## 05-Skeleton
1. Hook
2. Context
3. Constraint
4. Action / system
5. Trade-off
6. Translation sentence *(check depth gradient L1-L4)*
7. Invitation *(specific question)*

---

## 06-Invitation Rules *(CTA)*
- **Good:** “Where would this fail in your stack?”
- **Bad:** “Agree?” / “Thoughts?”

> **Never ask for validation—ask for holes.**

---

## 07-Voice
- One voice per post; tag #client-work if company context matters.
- Tone: confident, constrained, never absolute.

---

## 08-Timing
- Publish when you have outcome + constraint + trade-off.
- Hard ceiling: 1 post/day.
- Windows *(re-check each quarter)*:
  - 08:45-09:55 AM
  - 12:45 PM
  - 04:45-05:00 PM

---

## 09-Hashtags
- 3–5 only; move extras to first comment.
- Mix: 1 broad, 1 niche, 1 geo/role if relevant.

---

## 10-Evergreen Ratio
- ≥ 60% posts should be valid in two years.
- Mark draft with 🌲 or 🕒 before publishing.

---

## 11-KillList *(do NOT post)*
- AI screenshots or hype-driven AI/ML takes without production scars
- “X is changing everything” filler
- Tool lists without trade-offs
- Benchmark brags sans context
- Sanitized failures with no cost
- Success stories without “what got worse”
- Generic career advice
- Empty polls or “Agree?” endings
- Trend commentary you haven’t touched in prod

---

## 12-Templates
> **Use template → match outcome → fill skeleton.**

1. Contrarian
2. Failure-first
3. Comparison
4. Reduction
5. Temporal
6. Pattern-reveal
7. Architecture deep-dive
8. Opinionated reflection
9. Infra / ops

> *(Engagement-first template removed; ask narrow questions inside substantive posts instead.)*

---

## 12b-Pipeline *(Capture → Filter → Deploy)*

### Capture
- Dump raw ideas into notes *(Obsidian/Notion/voice memo)*.
- Tag hook & template if obvious.

### Filter *(mandatory gate)*
- Run KillList audit → fail = discard.
- Assign single outcome & single template.
- Ensure ≥ L1 insight + translation sentence.
- Label 🌲 or 🕒.

### Deploy
- Draft inside skeleton *(section 05)*.
- Pre-flight checklist: audience, outcome, voice, invitation, hashtags, media, links moved to comment.
- Schedule in LinkedIn native or buffer; obey timing windows *(08)*.
- Within 30 min: reply to first 5 comments with substance; add one clarifying self-comment.

### Post-Mortem *(24 h)*
- Log sentence that drove best thread + drop-off point.
- Update swipe file.

### Weekly Review
- Prune stale ideas; ladder high-performers into multi-post arc within 7 days.

---

## 13-Swipe-File
**Contrarian hook real example:**
> "Kubernetes is overrated for 90% of infra. Here’s the constraint that changed my mind…"
→ 42% engagement from staff+ engineers, 0 vendor fluff.

---

## 14-Metrics That Matter
- Track only:
  - Comments you’d happily defend in a design review
  - DMs that convert to 30-min calls
- Ignore impressions & ER; log conversions monthly to spot ROI trends without polluting creative decisions.

---

## 15-Post-Mortem Loop *(24 h)*
- Which sentence drove good comments?
- Where did skimmers stop?
- Update swipe file with learnings.

---

## 16-Final-Gate
> Read the post, then ask:
> “If a future hiring manager sees this, does my rate go up or down?”
> **Down → kill.**

---

## 17-Boring-Test
> “Does this make the system more boring?”
> **Yes → ship.**
> **No → bake longer.**

---

## 18-Versioning
- This file stays in `LinkedIn_Posting_RuleBook_v3.1.md` on main branch.
- Tag releases v3.2, v3.3 … quarterly after rerun & prune.
- Changelog at bottom of file.

---

## 19-Changelog

### v3.1 *(2026-01-09)*
- Added 12b-Pipeline *(Capture → Filter → Deploy)*
- Added depth-reminder in skeleton *(L1-L4 check)*
- Regex-friendly numeric prefix enforced *(no spaces)*
- KillList: explicit “hype-driven AI/ML without prod scars” rule
- Metrics: clarified conversion-only logging

### v3.0 *(2026-01-09)*
- Removed engagement-first template
- Deleted vanity KPI section
- Merged voice rules *(individual + company)*
- Swipe file added
- Hashtag cap 3–5
- Frequency rule → quality gate

Compounding >  Virality
----
01-Principles
•  One outcome per post (pick before you write).
•  Clarity + brevity; whitespace is free.
•  Every technical claim carries a constraint or failure mode.
•  If it isn’t boring enough to run in prod, it isn’t ready.
----
02-Outcome-Picker (choose one)
Authority | Network | Relationship | Opportunity | Idea-test
No outcome → no post.
----
03-Hook-Menu (first 2 lines)
Contrarian • Failure-first • Comparison • Reduction • Temporal • Pattern-reveal
No hook → rewrite.
----
04-Depth-Gradient (never start at 3)
1.  Why it matters
2.  How it works (concept)
3.  Implementation
4.  Where it breaks
Include one translation sentence for L3-4.
----
05-Skeleton
1.  Hook
2.  Context
3.  Constraint
4.  Action / system
5.  Trade-off
6.  Translation sentence (check depth gradient L1-L4)
7.  Invitation (specific question)
----
06-Invitation Rules (CTA)
Good: “Where would this fail in your stack?”
Bad: “Agree?” / “Thoughts?”
Never ask for validation—ask for holes.
----
07-Voice
One voice per post; tag #client-work if company context matters.
Tone: confident, constrained, never absolute.
----
08-Timing
Publish when you have outcome + constraint + trade-off.
Hard ceiling: 1 post/day.
Windows (re-check each quarter):
08:45-09:55 AM • 12:45 PM • 04:45-05:00 PM
----
09-Hashtags
3–5 only; move extras to first comment.
Mix: 1 broad, 1 niche, 1 geo/role if relevant.
----
10-Evergreen Ratio
≥ 60 % posts should be valid in two years.
Mark draft with 🌲 or 🕒 before publishing.
----
11-KillList (do NOT post)
•  AI screenshots or hype-driven AI/ML takes without production scars
•  “X is changing everything” filler
•  Tool lists without trade-offs
•  Benchmark brags sans context
•  Sanitized failures with no cost
•  Success stories without “what got worse”
•  Generic career advice
•  Empty polls or “Agree?” endings
•  Trend commentary you haven’t touched in prod
----
12-Templates
Use template → match outcome → fill skeleton.
Swiped examples are collapsed under each template in the source file; expand on demand.
1.  Contrarian
2.  Failure-first
3.  Comparison
4.  Reduction
5.  Temporal
6.  Pattern-reveal
7.  Architecture deep-dive
8.  Opinionated reflection
9.  Infra / ops
(Engagement-first template removed; ask narrow questions inside substantive posts instead.)
----
12b-Pipeline (Capture → Filter → Deploy)
Capture
•  Dump raw ideas into notes (Obsidian/Notion/voice memo).
•  Tag hook & template if obvious.
Filter (mandatory gate)
•  Run KillList audit → fail = discard.
•  Assign single outcome & single template.
•  Ensure ≥ L1 insight + translation sentence.
•  Label 🌲 or 🕒.
Deploy
•  Draft inside skeleton (section 05).
•  Pre-flight checklist: audience, outcome, voice, invitation, hashtags, media, links moved to comment.
•  Schedule in LinkedIn native or buffer; obey timing windows (08).
•  Within 30 min: reply to first 5 comments with substance; add one clarifying self-comment.
Post-Mortem (24 h)
•  Log sentence that drove best thread + drop-off point.
•  Update swipe file.
Weekly Review
•  Prune stale ideas; ladder high-performers into multi-post arc within 7 days.
----
13-Swipe-File
Contrarian hook real example:
"Kubernetes is overrated for 90 % of infra. Here’s the constraint that changed my mind…"
→ 42 % engagement from staff+ engineers, 0 vendor fluff.
----
14-Metrics That Matter
Track only:
•  Comments you’d happily defend in a design review
•  DMs that convert to 30-min calls
Ignore impressions & ER; log conversions monthly to spot ROI trends without polluting creative decisions.
----
15-Post-Mortem Loop (24 h)
•  Which sentence drove good comments?
•  Where did skimmers stop?
•  Update swipe file with learnings.
----
16-Final-Gate
Read the post, then ask:
“If a future hiring manager sees this, does my rate go up or down?”
Down → kill.
----
17-Boring-Test
“Does this make the system more boring?”
Yes → ship.
No → bake longer.
----
18-Versioning
This file stays in LinkedIn_Posting_RuleBook_v3.1.md on main branch.
Tag releases v3.2, v3.3 … quarterly after rerun & prune.
Changelog at bottom of file.
----
19-Changelog
v3.1 (2026-01-09)
•  Added 12b-Pipeline (Capture → Filter → Deploy)
•  Added depth-reminder in skeleton (L1-L4 check)
•  Regex-friendly numeric prefix enforced (no spaces)
•  KillList: explicit “hype-driven AI/ML without prod scars” rule
•  Metrics: clarified conversion-only logging
v3.0 (2026-01-09)
•  Removed engagement-first template
•  Deleted vanity KPI section
•  Merged voice rules (individual + company)
•  Swipe file added
•  Hashtag cap 3–5
•  Frequency rule → quality gate
