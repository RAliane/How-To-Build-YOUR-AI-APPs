❤️ Healthcheck Templates

Liveness • Readiness • Dependency Awareness

⸻

1. Healthcheck Design Rules (Read This Once)

Every service must expose:
	•	/health/live → process alive
	•	/health/ready → safe to receive traffic
	•	/health/deps → can reach required dependencies

Healthchecks must:
	•	Return 200 or 503 only
	•	Be cheap
	•	Have no side effects
	•	Never mutate state
	•	Never depend on edge traffic

⸻

2. Standard Healthcheck Response Schema
```json
{
  "status": "ok",
  "service": "rust-api",
  "version": "1.3.2",
  "uptime_sec": 18423,
  "timestamp": "2026-01-10T19:22:01Z"
}

When unhealthy:

{
  "status": "degraded",
  "failed": ["postgres", "redis"]
}
```

⸻

3. Rust (Axum / Actix) Healthcheck Template

Routes
```
use std::time::Instant;
use axum::{routing::get, Json, Router};

static START: once_cell::sync::Lazy<Instant> =
    once_cell::sync::Lazy::new(Instant::now);

pub fn health_routes() -> Router {
    Router::new()
        .route("/health/live", get(live))
        .route("/health/ready", get(ready))
}

async fn live() -> Json<serde_json::Value> {
    Json(json!({
        "status": "ok",
        "uptime_sec": START.elapsed().as_secs()
    }))
}

async fn ready() -> Result<Json<serde_json::Value>, axum::http::StatusCode> {
    if postgres_ok().await {
        Ok(Json(json!({ "status": "ok" })))
    } else {
        Err(axum::http::StatusCode::SERVICE_UNAVAILABLE)
    }
}
```
📌 Liveness never fails unless the process is dead
📌 Readiness checks DB connectivity only

⸻

4. FastAPI Healthcheck Template
```
from fastapi import FastAPI, status
from fastapi.responses import JSONResponse
import time

app = FastAPI()
START = time.time()

@app.get("/health/live")
def live():
    return {
        "status": "ok",
        "uptime_sec": int(time.time() - START)
    }

@app.get("/health/ready")
def ready():
    if not db_ok():
        return JSONResponse(
            status_code=status.HTTP_503_SERVICE_UNAVAILABLE,
            content={"status": "degraded", "failed": ["postgres"]}
        )
    return {"status": "ok"}
```

⸻

5. Postgres Healthcheck (Container-Level)
```
healthcheck:
  test: ["CMD-SHELL", "pg_isready -U app"]
  interval: 30s
  timeout: 5s
  retries: 3
```
No SQL. No writes. Just readiness.

⸻

6. Redis Healthcheck
```
healthcheck:
  test: ["CMD", "redis-cli", "ping"]
  interval: 30s
```

⸻

7. MinIO Healthcheck
```
healthcheck:
  test: ["CMD", "curl", "-f", "http://localhost:9000/minio/health/live"]
  interval: 30s
```

⸻

8. Nginx Healthcheck
```
healthcheck:
  test: ["CMD", "nginx", "-t"]
  interval: 30s
```

⸻

🧾 Postmortem Template

Blameless • Actionable • Deterministic

⸻

1. Postmortem Rules
	•	No blame
	•	No opinions
	•	No “we think”
	•	No vibes
	•	Facts only
	•	Every incident ends with concrete actions

⸻

2. File Name Convention
```
postmortems/
  2026-01-10-api-outage.md
```

⸻

3. Postmortem Template (Markdown)
```
# Postmortem: <Short Incident Title>

**Date:** 2026-01-10  
**Duration:** 17 minutes  
**Severity:** SEV-2  
**Status:** Resolved  

---

## Summary

At <time>, <service> experienced <failure>.
The issue was detected by <healthcheck/monitor>.
Service was restored at <time>.

---

## Impact

- % of users affected
- What functionality was unavailable
- Data loss: Yes / No

---

## Timeline (UTC)

| Time | Event |
|-----|------|
| 19:02 | Alert fired: readiness check failed |
| 19:05 | On-call acknowledged |
| 19:09 | Root cause identified |
| 19:19 | Fix deployed |
| 19:21 | Healthchecks green |

---

## Root Cause

**What failed:**  
- Example: Postgres connection pool exhausted

**Why it failed:**  
- Missing max connection limits
- Traffic spike exceeded assumptions

---

## Detection

- How was the incident detected?
- Which healthcheck failed?
- Was detection delayed?

---

## Resolution

- What action restored service?
- Was a rollback needed?

---

## What Went Well

- Fast detection
- Clear logs
- Safe rollback path

---

## What Went Wrong

- No alert on connection saturation
- Missing load testing

---

## Action Items (Required)

| Action | Owner | Priority | Due |
|------|------|----------|-----|
| Add DB pool metrics | @you | High | 2026-01-15 |
| Add readiness timeout | @you | Medium | 2026-01-20 |

---

## Lessons Learned

- Explicit limits > defaults
- DB pressure must be observable
```

⸻

4. Severity Definitions (Standardized)
```
Level	Meaning
SEV-1	Full outage / data loss
SEV-2	Partial outage
SEV-3	Degraded performance
SEV-4	Minor issue
```

⸻

5. Golden Rule (Again)

If an incident did not produce action items, the postmortem is invalid.

⸻
Here’s your polished and consistently formatted **Healthcheck Templates** markdown file, with improved readability, structure, and clarity:

```markdown
# ❤️ Healthcheck Templates

**Liveness • Readiness • Dependency Awareness**

---

## 1. Healthcheck Design Rules

Every service must expose:
- `/health/live` → process alive
- `/health/ready` → safe to receive traffic
- `/health/deps` → can reach required dependencies

**Healthchecks must:**
- Return 200 or 503 only
- Be cheap
- Have no side effects
- Never mutate state
- Never depend on edge traffic

---

## 2. Standard Healthcheck Response Schema

**Healthy:**
```json
{
  "status": "ok",
  "service": "rust-api",
  "version": "1.3.2",
  "uptime_sec": 18423,
  "timestamp": "2026-01-10T19:22:01Z"
}
```

**Unhealthy:**
```json
{
  "status": "degraded",
  "failed": ["postgres", "redis"]
}
```

---

## 3. Rust (Axum / Actix) Healthcheck Template

```rust
use std::time::Instant;
use axum::{routing::get, Json, Router};

static START: once_cell::sync::Lazy<Instant> =
    once_cell::sync::Lazy::new(Instant::now);

pub fn health_routes() -> Router {
    Router::new()
        .route("/health/live", get(live))
        .route("/health/ready", get(ready))
}

async fn live() -> Json<serde_json::Value> {
    Json(json!({
        "status": "ok",
        "uptime_sec": START.elapsed().as_secs()
    }))
}

async fn ready() -> Result<Json<serde_json::Value>, axum::http::StatusCode> {
    if postgres_ok().await {
        Ok(Json(json!({ "status": "ok" })))
    } else {
        Err(axum::http::StatusCode::SERVICE_UNAVAILABLE)
    }
}
```
> **Note:**
> - Liveness never fails unless the process is dead
> - Readiness checks DB connectivity only

---

## 4. FastAPI Healthcheck Template

```python
from fastapi import FastAPI, status
from fastapi.responses import JSONResponse
import time

app = FastAPI()
START = time.time()

@app.get("/health/live")
def live():
    return {
        "status": "ok",
        "uptime_sec": int(time.time() - START)
    }

@app.get("/health/ready")
def ready():
    if not db_ok():
        return JSONResponse(
            status_code=status.HTTP_503_SERVICE_UNAVAILABLE,
            content={"status": "degraded", "failed": ["postgres"]}
        )
    return {"status": "ok"}
```

---

## 5. Container Healthchecks

### Postgres
```yaml
healthcheck:
  test: ["CMD-SHELL", "pg_isready -U app"]
  interval: 30s
  timeout: 5s
  retries: 3
```
> No SQL. No writes. Just readiness.

### Redis
```yaml
healthcheck:
  test: ["CMD", "redis-cli", "ping"]
  interval: 30s
```

### MinIO
```yaml
healthcheck:
  test: ["CMD", "curl", "-f", "http://localhost:9000/minio/health/live"]
  interval: 30s
```

### Nginx
```yaml
healthcheck:
  test: ["CMD", "nginx", "-t"]
  interval: 30s
```

---

# 🧾 Postmortem Template

**Blameless • Actionable • Deterministic**

---

## 1. Postmortem Rules

- No blame
- No opinions
- No “we think”
- No vibes
- Facts only
- Every incident ends with concrete actions

---

## 2. File Name Convention

```
postmortems/
  2026-01-10-api-outage.md
```

---

## 3. Postmortem Template (Markdown)

```markdown
# Postmortem: <Short Incident Title>

**Date:** 2026-01-10
**Duration:** 17 minutes
**Severity:** SEV-2
**Status:** Resolved

---

## Summary

At <time>, <service> experienced <failure>.
The issue was detected by <healthcheck/monitor>.
Service was restored at <time>.

---

## Impact

- % of users affected
- What functionality was unavailable
- Data loss: Yes / No

---

## Timeline (UTC)

| Time     | Event                          |
|----------|--------------------------------|
| 19:02    | Alert fired: readiness check failed |
| 19:05    | On-call acknowledged           |
| 19:09    | Root cause identified          |
| 19:19    | Fix deployed                   |
| 19:21    | Healthchecks green             |

---

## Root Cause

**What failed:**
- Example: Postgres connection pool exhausted

**Why it failed:**
- Missing max connection limits
- Traffic spike exceeded assumptions

---

## Detection

- How was the incident detected?
- Which healthcheck failed?
- Was detection delayed?

---

## Resolution

- What action restored service?
- Was a rollback needed?

---

## What Went Well

- Fast detection
- Clear logs
- Safe rollback path

---

## What Went Wrong

- No alert on connection saturation
- Missing load testing

---

## Action Items (Required)

| Action                | Owner | Priority | Due        |
|-----------------------|-------|----------|------------|
| Add DB pool metrics   | @you  | High     | 2026-01-15 |
| Add readiness timeout | @you  | Medium   | 2026-01-20 |

---

## Lessons Learned

- Explicit limits > defaults
- DB pressure must be observable
```

---

## 4. Severity Definitions

| Level | Meaning                |
|-------|------------------------|
| SEV-1 | Full outage / data loss|
| SEV-2 | Partial outage          |
| SEV-3 | Degraded performance   |
| SEV-4 | Minor issue            |

---

## 5. Golden Rule

> If an incident did not produce action items, the postmortem is invalid.

---

## 6. Final Thought

**Healthchecks prevent silent failure.**
**Postmortems prevent repeat failure.**

Most teams do neither properly.
You now have institutional memory in markdown.


---
6. Final Thought

Healthchecks prevent silent failure.
Postmortems prevent repeat failure.

Most teams do neither properly.
You now have institutional memory in markdown.
