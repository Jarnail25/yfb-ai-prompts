# Architecture Decisions — Your Fitness Buddy

This document records architectural decisions and their rationale. Reference this when making implementation choices that depend on understanding **why** the architecture is the way it is, not just **what** it is.

---

## Multi-Repo Architecture

**Decision:** Three separate repositories (yfb-frontend, yfb-backend, yfb-ai-prompts).

**Why not monorepo:**
- The backend (Supabase) can be reused by a mobile app later without carrying frontend dependencies.
- AI prompts are core IP and need independent versioning. Prompt changes should be tracked separately from code changes, with their own changelog.
- Different deploy pipelines: frontend deploys independently, backend deploys manually via Supabase CLI, prompts have no direct deployment (bundled into Edge Functions at backend deploy time).

**Tradeoff accepted:** Shared types between frontend and backend must be manually synchronized. The contract-first approach (API contracts documented in commit messages) mitigates this.

---

## Why Supabase (Backend)

**Decision:** Supabase (PostgreSQL + Edge Functions + Auth + Storage + Realtime).

**Reasons:**
- PostgreSQL with Row Level Security (RLS) provides fine-grained access control without application-level auth checks. Every query is automatically scoped to the authenticated user.
- Edge Functions (Deno/TypeScript) run close to the database — no cold start + network hop penalty.
- Auth is built-in with email/password, magic link, and OAuth. No separate auth service needed.
- Realtime subscriptions enable live dashboard updates without polling.
- Storage for user uploads (blood panel PDFs, profile photos).
- Local development via `supabase start` gives a full Postgres + Auth + Functions stack locally.

**What Supabase does NOT handle well:**
- Complex background jobs (would need a separate queue system at scale — not needed for personal use).

**Tradeoff accepted:** Vendor lock-in to Supabase's Edge Functions runtime (Deno, not Node.js). Migration to another backend would require rewriting Edge Functions. Acceptable because the data layer (PostgreSQL) is portable.

---

## Why Claude API (AI Layer)

**Decision:** Anthropic Claude API, called exclusively from Supabase Edge Functions.

**Model selection:**
- **Claude Opus** for plan generation: highest reasoning capability needed for complex periodization decisions. Temperature 0.3 (deterministic). Max 16,000 output tokens. Infrequent (once per 12-week cycle).
- **Claude Sonnet** for coach chat: fast response times, streaming. Temperature 0.5. Max 500 output tokens.
- **Claude Sonnet** for supplement analysis: analytical task, moderate complexity. Temperature 0.2. Max 2,000 output tokens. Infrequent.

**Why not OpenAI / other providers:**
- Opus reasoning quality for periodization logic exceeds GPT-4o for structured, domain-specific output.
- Single provider simplifies API key management, error handling, and cost tracking.

**Architecture rule:** Frontend NEVER calls Claude directly. All AI requests go through Edge Functions which handle: authentication, token budget enforcement, prompt assembly, response parsing against output schemas, and cost logging.

---

## Data Flow Architecture

```
User Browser
    │
    ▼
[Next.js App]  ──── Server Components (SSR) ────►  Supabase Client (reads, RLS-scoped)
    │
    │ (user actions)
    ▼
[Supabase Edge Functions]  ◄──────────────  [PostgreSQL + RLS]
    │
    ├── generate-plan/       → Claude Opus API  → parse output-schema.json → store plan
    ├── coach-chat/          → Claude Sonnet API → stream response
    ├── renpho-sync/         → Renpho API → store body comp data
    └── analyze-blood-panel/ → Claude Sonnet API → supplement recommendations
```

**Key principle:** The database is the single source of truth. Edge Functions are stateless processors. The frontend is a read-heavy client that triggers Edge Functions for writes and AI operations.

---

## PWA / Offline Strategy

**Decision:** Progressive Web App with offline support for session tracking.

**What works offline:** Current session exercise list, set logging, RPE input, rest timer.
**What requires connectivity:** Coach chat, plan generation, dashboard sync.

**Sync strategy:** Last-write-wins with `synced_at` timestamp and `device_id`. Offline data stored in IndexedDB via Workbox. Syncs on reconnection.

**Tradeoff accepted:** Last-write-wins can lose data if the same session is edited on two devices while both are offline. Acceptable for single-user personal tool.

---

*Update this document when architectural decisions change.*
