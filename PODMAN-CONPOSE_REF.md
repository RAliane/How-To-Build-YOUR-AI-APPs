# 🧱 SUPERSTACK — Podman Compose Reference

**Zero-Trust • Triple Network • Deterministic**

---

## 1. Networks *(Defined First, Always)*

```yaml
networks:
  edge-net:
    driver: bridge
  auth-net:
    driver: bridge
    internal: true
  db-net:
    driver: bridge
    internal: true
```

**Rules Enforced:**
- `internal: true` blocks external routing
- DB never exposed
- Edge can only see edge
- Auth is the only bridge

---

## 2. Volumes *(Explicit, Named, Deterministic)*

```yaml
volumes:
  pgdata:
  minio-data:
  redis-data:
  vault-data:
  ollama-data:
```

> **No anonymous volumes. Ever.**

---

## 3. Reverse Proxy *(Nginx – Edge Only)*

```yaml
services:
  nginx:
    image: nginx:alpine
    container_name: nginx
    restart: unless-stopped
    networks:
      - edge-net
      - auth-net
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./infra/nginx/nginx.conf:/etc/nginx/nginx.conf:ro
      - ./infra/nginx/certs:/etc/letsencrypt
    depends_on:
      - directus
      - hasura
    healthcheck:
      test: ["CMD", "nginx", "-t"]
      interval: 30s
      timeout: 5s
      retries: 3
```

✅ **TLS**
✅ **Rate limiting**
✅ **Load balancing**
❌ **No DB access**

---

## 4. Directus *(Auth-Net Only)*

```yaml
  directus:
    image: directus/directus:latest
    container_name: directus
    restart: unless-stopped
    networks:
      - auth-net
      - db-net
    environment:
      DIRECTUS_DATABASE_CLIENT: pg
      DIRECTUS_DATABASE_HOST: postgres
      DIRECTUS_DATABASE_NAME: directus
    secrets:
      - db_password
    depends_on:
      - postgres
    healthcheck:
      test: ["CMD", "wget", "--spider", "http://localhost:8055/server/health"]
      interval: 30s
```

📌 **CRUD, flows, admin**
📌 **Never exposed directly**

---

## 5. Hasura *(Auth-Net Only)*

```yaml
  hasura:
    image: hasura/graphql-engine:latest
    container_name: hasura
    restart: unless-stopped
    networks:
      - auth-net
      - db-net
    environment:
      HASURA_GRAPHQL_DATABASE_URL: postgres://hasura@postgres:5432/app
      HASURA_GRAPHQL_ENABLE_CONSOLE: "false"
    secrets:
      - hasura_admin_secret
    depends_on:
      - postgres
```

📌 **High-throughput GraphQL**
📌 **No ORM nonsense**
📌 **SQL remains king**

---

## 6. Postgres *(DB-Net Only)*

```yaml
  postgres:
    image: postgres:16-alpine
    container_name: postgres
    restart: unless-stopped
    networks:
      - db-net
    volumes:
      - pgdata:/var/lib/postgresql/data
      - ./infra/postgres/init:/docker-entrypoint-initdb.d
    environment:
      POSTGRES_DB: app
      POSTGRES_USER: app
    secrets:
      - db_password
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U app"]
      interval: 30s
```

**Extensions installed in init scripts:**
- pgvector
- pg_edge_vectorizer
- postgis *(only when needed)*

---

## 7. Redis *(Optional, DB-Net Only)*

```yaml
  redis:
    image: redis:alpine
    container_name: redis
    restart: unless-stopped
    networks:
      - db-net
    volumes:
      - redis-data:/data
    command: ["redis-server", "--appendonly", "yes"]
```

📌 **Cache / ephemeral state**
📌 **Not your DB**

---

## 8. MinIO *(Object Storage, DB-Net Only)*

```yaml
  minio:
    image: minio/minio
    container_name: minio
    restart: unless-stopped
    networks:
      - db-net
    volumes:
      - minio-data:/data
    command: server /data --console-address ":9001"
    secrets:
      - minio_root_user
      - minio_root_password
```

📌 **Static assets**
📌 **Cold storage**
📌 **Not a database**

---

## 9. Rust Services *(Auth-Net Only)*

```yaml
  rust-api:
    build:
      context: ./services/rust-api
      dockerfile: Containerfile
    container_name: rust-api
    restart: unless-stopped
    networks:
      - auth-net
      - db-net
    environment:
      RUST_LOG: info
    depends_on:
      - postgres
```

📌 **Async orchestration**
📌 **MCP / MoE routing**
📌 **Deterministic binaries**

---

## 10. Python FastAPI *(Only If Required)*

```yaml
  fastapi:
    build:
      context: ./services/fastapi
      dockerfile: Containerfile
    container_name: fastapi
    restart: unless-stopped
    networks:
      - auth-net
      - db-net
```

⚠ **Uses uv, not pip**
⚠ **Only when Rust isn’t suitable**

---

## 11. Vault *(Secrets Backbone)*

```yaml
  vault:
    image: hashicorp/vault
    container_name: vault
    restart: unless-stopped
    networks:
      - auth-net
    volumes:
      - vault-data:/vault/data
```

📌 **Central secrets**
📌 **Rotation capable**
📌 **No plaintext envs**

---

## 12. Ollama *(Local AI)*

```yaml
  ollama:
    image: ollama/ollama
    container_name: ollama
    restart: unless-stopped
    networks:
      - auth-net
    volumes:
      - ollama-data:/root/.ollama
```

📌 **Local embeddings**
📌 **API cost control**
📌 **RAG foundation**

---

## 13. Secrets *(Never Inline)*

```yaml
secrets:
  db_password:
    file: ./secrets/db_password.txt
  hasura_admin_secret:
    file: ./secrets/hasura_admin_secret.txt
  minio_root_user:
    file: ./secrets/minio_user.txt
  minio_root_password:
    file: ./secrets/minio_password.txt
```

---

## 14. Final Mental Model

```
[ Internet ]
     ↓
  edge-net
     ↓
  nginx
     ↓
  auth-net
     ↓
 Directus / Hasura / Rust
     ↓
  db-net
     ↓
 Postgres / Redis / MinIO
```

> **No shortcuts.**
> **No hope-based routing.**
> **No “just for now” ports.**

---

## 15. Golden Rule

> If a service does not need to talk to another service, they do **not** share a network.
