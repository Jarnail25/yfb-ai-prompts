# Architecture Decisions — Your Fitness Buddy

This document records architectural decisions and their rationale. Agents reference this when making implementation choices that depend on understanding **why** the architecture is the way it is, not just **what** it is.

---

## Multi-Repo Architecture

**Decision:** Three separate repositories (yfb-frontend, yfb-backend, yfb-ai-prompts).

**Why not monorepo:**
- Two AI agents could need to edit the same files simultaneously in later sprints. Separate repos prevent merge conflicts between agents working in parallel.
- The backend (Supabase) could be reused by a mobile app later without carrying frontend dependencies.
- AI prompts are core IP and need independent versioning. Prompt changes should be tracked separately from code changes, with their own changelog.
- Different deploy pipelines: frontend auto-deploys to Vercel on push, backend deploys manually via Supabase CLI, prompts have no direct deployment (bundled into Edge Functions at backend deploy time).

**Tradeoff accepted:** Shared types between frontend and backend must be manually synchronized. There is no shared `types/` package. The contract-first development protocol (API contracts documented in commit messages) mitigates this.

---

## Why Vercel (Frontend Hosting)

**Decision:** Next.js on Vercel.

**Reasons:**
- Automatic preview deployments per PR — every branch gets a live URL for review.
- Zero-config Next.js deployment (App Router, Server Components, Image Optimization).
- Edge middleware for auth checks and redirects without a server round-trip.
- Built-in Web Vitals monitoring.
- Free tier covers MVP; scales predictably.

**What Vercel does NOT handle:**
- Database operations (all go through Supabase Edge Functions).
- AI API calls (all go through Supabase Edge Functions — keeps API keys server-side).
- Webhook handlers (Stripe, integrations — handled by Supabase Edge Functions).

---

## Why Supabase (Backend)

**Decision:** Supabase (PostgreSQL + Edge Functions + Auth + Storage + Realtime).

**Reasons:**
- PostgreSQL with Row Level Security (RLS) provides fine-grained access control without application-level auth checks. Every query is automatically scoped to the authenticated user.
- Edge Functions (Deno/TypeScript) run close to the database — no cold start + network hop penalty that Vercel serverless functions would have for DB operations.
- Auth is built-in with email/password, magic link, and OAuth. No separate auth service needed.
- Realtime subscriptions enable live dashboard updates without polling.
- Storage for user uploads (blood panel PDFs, profile photos).
- Local development via `supabase start` gives a full Postgres + Auth + Functions stack locally.

**What Supabase does NOT handle well:**
- Complex background jobs (would need a separate queue system at scale — not needed for MVP).
- Full-text search across large datasets (would need external search service at scale).

**Tradeoff accepted:** Vendor lock-in to Supabase's Edge Functions runtime (Deno, not Node.js). Migration to another backend would require rewriting Edge Functions. Acceptable because the data layer (PostgreSQL) is portable.

---

## Why Claude API (AI Layer)

**Decision:** Anthropic Claude API, called exclusively from Supabase Edge Functions.

**Model selection:**
- **Claude Opus** for plan generation: highest reasoning capability needed for complex periodization decisions. Temperature 0.3 (deterministic). Max 12,000 output tokens. Cost: highest per call, but infrequent (once per 12-week cycle per user).
- **Claude Sonnet** for coach chat: fast response times, good enough reasoning for conversational coaching. Temperature 0.5. Max 500 output tokens. Cost: moderate per call, high frequency.
- **Claude Sonnet** for supplement analysis: analytical task, moderate complexity. Temperature 0.2. Max 2,000 output tokens. Infrequent.

**Why not OpenAI / other providers:**
- Opus reasoning quality for periodization logic exceeds GPT-4o for structured, domain-specific output.
- Single provider simplifies API key management, error handling, and cost tracking.
- Anthropic's safety layer aligns with health/fitness content requirements.

**Architecture rule:** Frontend NEVER calls Claude directly. All AI requests go through Edge Functions which handle: authentication, rate limiting, token budget enforcement, prompt assembly (loading prompts from yfb-ai-prompts), response parsing against output schemas, and cost logging.

---

## Why Multi-Agent Development

**Decision:** Specialized AI agents (Frontend, Backend, AI, Integration, Full-Stack, DevOps) working sequentially through sprints.

**Why not single agent:**
- Context window limits mean a single agent cannot hold the full PRD + Tech Guide + all code in context. Specialized agents load only their repo's CLAUDE.md + relevant docs.
- File ownership boundaries prevent an AI agent from making changes it shouldn't (e.g., Frontend Agent shouldn't write SQL). Enforced by CLAUDE.md rules + `.claude/hooks.json` Exit Code 2 hooks.
- Session handoffs via SESSION_LOGS.md provide audit trail and prevent context loss between sessions.

**Tradeoff accepted:** Sequential development is slower than parallel. For MVP with a solo founder, sequential is safer — fewer merge conflicts, clearer debugging when something breaks. Parallel sessions can be introduced in Sprint 3+ once the foundation is stable.

---

## Data Flow Architecture

```
User Browser
    │
    ▼
[Next.js on Vercel]  ──── Server Components (SSR) ────►  Supabase Client (reads)
    │                                                          │
    │ (user actions)                                           │ (RLS-scoped queries)
    ▼                                                          ▼
[Supabase Edge Functions]  ◄──────────────────────────  [PostgreSQL + RLS]
    │
    ├── generate-plan/     → Claude Opus API  → parse output-schema.json → store plan
    ├── coach-chat/        → Claude Sonnet API → stream response
    ├── stripe-webhook/    → Stripe signature verify → update subscription
    ├── stripe-checkout/   → create Stripe session → return URL
    ├── renpho-sync/       → Renpho API → store body comp data
    └── analyze-blood-panel/ → Claude Sonnet API → supplement recommendations
```

**Key principle:** The database is the single source of truth. Edge Functions are stateless processors. The frontend is a read-heavy client that triggers Edge Functions for writes and AI operations.

---

## PWA / Offline Strategy

**Decision:** Progressive Web App with offline support for session tracking.

**What works offline:** Current session exercise list, set logging, RPE input, rest timer.
**What requires connectivity:** Coach chat, plan generation, dashboard sync, marketplace.

**Sync strategy:** Last-write-wins with `synced_at` timestamp and `device_id`. Offline data stored in IndexedDB via Workbox. Syncs on reconnection.

**Tradeoff accepted:** Last-write-wins can lose data if the same session is edited on two devices while both are offline. Acceptable for MVP with 2 users. See `YFB_Future_Roadmap.md` item 7 for field-level conflict resolution plan at scale.

---

*This document should be updated when architectural decisions change. Agents should reference it when making implementation choices that touch system boundaries.*
