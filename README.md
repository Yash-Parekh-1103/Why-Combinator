# Why-Combinator

Simple, task-first guidance to build a scalable product with a normal website plus an AI backend.

## Goal
Build a reliable web product that can handle ~1k concurrent users without crashing, with a separate AI service using LangChain + Ollama + FastAPI.

---

## Recommended Tech Stack (by part)

### AI Backend (required)
- **FastAPI** for the AI service API
- **LangChain** for orchestration
- **Ollama** for local model serving

### Normal Website (non-AI part)
**Best choice: Next.js**
- Full website + API routes in one place
- Server-side rendering and SEO
- Built-in performance features (image optimization, caching, streaming)

**When to choose Express instead**
- You only want a pure API backend
- You already have a separate frontend (React/Vue/etc.)

**Decision**: Use **Next.js** for the normal website, and keep **FastAPI** for the AI service.

---

## Recommended Folder Structure (production-ready)

```
why-combinator/
  apps/
    web/                # Next.js app (normal website)
    ai-api/             # FastAPI + LangChain + Ollama
  packages/
    shared/             # shared types, utils, UI tokens
  infra/
    nginx/              # reverse proxy configs
    docker/             # dockerfiles, compose
  docs/
  scripts/
  .env.example
  README.md
```

---

## Task Roadmap (do in order)

### Phase 1 — Product Basics
1. Define pages and user flows for the normal website
2. Define AI endpoints (inputs/outputs) and rate limits
3. Set up repo structure and shared packages

### Phase 2 — Normal Website (Next.js)
1. Create Next.js app in `apps/web`
2. Build core pages (home, auth, dashboard, pricing, etc.)
3. Add basic API routes if needed (contact form, user profile)
4. Add authentication (e.g., NextAuth or custom JWT)

### Phase 3 — AI Service (FastAPI)
1. Create FastAPI app in `apps/ai-api`
2. Integrate LangChain + Ollama
3. Expose AI endpoints and validate inputs
4. Add request timeouts and rate limiting

### Phase 4 — Data Layer
1. Choose DB (Postgres recommended)
2. Add migrations
3. Add connection pooling

### Phase 5 — Scalability (for 1k+ concurrent users)
1. Put **Nginx** or **Cloudflare** in front
2. Add **Redis** for caching + rate limiting
3. Enable horizontal scaling (multiple app instances)
4. Add job queue for heavy AI tasks (e.g., Celery + Redis)
5. Add observability (logs, metrics, uptime checks)
6. Load test (k6 or Artillery) before launch

### Phase 6 — Deployment
1. Dockerize `web` and `ai-api`
2. Deploy on VPS or cloud (Fly.io, Render, AWS, etc.)
3. Add CI/CD for auto deploy
4. Set up backups and alerts

---

## Minimum Requirements to Avoid Crashes at 1k Concurrency

- **Horizontal scaling**: 2+ instances for web + AI services
- **Caching**: Redis for sessions and repeated AI queries
- **Timeouts + retries**: prevent stuck requests
- **Queue heavy AI jobs**: don’t block web threads
- **CDN** for static assets
- **Monitoring**: logs + performance alerts

---

## Next Step
Start with **Phase 1**, then build the **Next.js web app**, then the **FastAPI AI service**.
