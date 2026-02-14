TECHNICAL IMPLEMENTATION GUIDE
Your Fitness Buddy
Claude Code Multi-Agent Development Playbook
Version 2.1 | February 2026
Multi-Agent Orchestration | Session Coordination | Agent Guidelines
Agent Roles | Repository Structure | CLAUDE.md Specs | Session Orchestration | Task Breakdown
1. DEVELOPMENT STRATEGY & MULTI-AGENT ARCHITECTURE
1.1 Architecture Philosophy
Your Fitness Buddy is built by a solo developer using Claude Code with specialized agent roles. The project is split across three independent Git repositories, each with its own CLAUDE.md instruction file that defines agent behavior, coding rules, and file ownership boundaries.
This multi-agent approach solves three critical problems: context overflow (no single session can hold the entire project), consistency drift (agents follow repo-specific rules), and merge conflicts (strict file ownership prevents cross-agent interference).
1.2 The Three Repositories
1.3 Agent Roles
Each Claude Code session has ONE role. You declare the role at session start, and the agent focuses exclusively on that scope. When switching roles, start a NEW session with fresh context.
1.4 Critical Rules
An agent MUST NOT modify files outside its ownership scope. Frontend Agent never writes SQL. Backend Agent never touches React components. This is enforced by `.claude/hooks.json` (Exit Code 2 hooks block cross-repo file edits at the tool level).
Every session starts by reading the repo's CLAUDE.md file and `feature-tracker.json`. This is non-negotiable.
Every session ends with updating `feature-tracker.json` and appending a structured handoff summary to SESSION_LOGS.md (see Section 1.5).
All AI API calls happen in Edge Functions (yfb-backend). The frontend NEVER calls Claude API directly.
Shared TypeScript types live in yfb-frontend/src/types/ (canonical source). Backend uses equivalent Zod schemas. AI output schemas must match.
TypeScript strict mode (`tsconfig.json`) is NON-NEGOTIABLE. See `docs/ARCHITECTURE.md` for architectural decisions and rationale.
1.5 SESSION ORCHESTRATION & COORDINATION
1.5.1 Sequential vs. Parallel Sessions
For MVP (Phases 1–2): STRICTLY SEQUENTIAL sessions.
Complete one session, commit, push, then start the next session with fresh context referencing the previous output. This eliminates merge conflicts, context confusion, and coordination overhead.
Parallel sessions (Phase 3+ only) require:
Completely independent features in separate repos
No shared files between sessions
Stable architecture with well-defined boundaries
Separate git branches with regular sync points
Rule of thumb: If you need to think about coordination, use sequential sessions.
1.5.2 Sequential Session Flow Example
Building the Quiz Funnel feature end-to-end:
1.5.3 Dependency Handoff Pattern
When Task B depends on Task A's output, use this contract-first handoff:
SESSION A (creating the dependency):
Build the feature completely and test it.
Document the interface contract in the git commit message (URL, method, request/response schema, error codes).
Push to remote.
Write handoff note in SESSION_LOGS.md.
SESSION B (consuming the dependency):
Start session with explicit context referencing Session A's commit and contract.
Build against the documented interface (not the implementation).
Verify integration works end-to-end.
Commit with reference to the contract.
1.5.4 Session Start Template
Every new session begins with this prompt structure:
You are the [ROLE] Agent for Your Fitness Buddy. Read CLAUDE.md.
Read feature-tracker.json for current project state and blockers.
Context from previous session ([DATE], [AGENT]):
- Completed: [what was built]
- API contracts: [endpoints created with schemas]
- Known issues: [bugs or incomplete work]
- Current state: [files modified, features working]
Task: [specific task for this session]
1.5.5 Session End Template (Mandatory)
Every session ends by:
1. Updating `feature-tracker.json` with status changes, new contracts, and blockers.
2. Appending to SESSION_LOGS.md in the repo root:
## Session [N]: [DATE] - [AGENT ROLE]
Duration: [X] hours | Commits: [hashes] | Branch: [name]
### Completed
- [Feature/task built, files created/modified]
### Interface Contracts
- POST /functions/v1/endpoint - { request } -> { response }
- ComponentName - Props: { interface }
- Table: table_name - [purpose, columns added]
### Known Issues
- [Bugs, workarounds, tech debt]
### Next Session
- Recommended agent: [role]
- Strategy: Sequential / Can parallel with [X]
- Tasks: 1) [...] 2) [...] 3) [...]
### Handoff Notes
- [Gotchas, decisions made, context the next agent needs]
1.5.6 Conflict Recovery
If sessions accidentally touch the same files:
Stop both sessions immediately.
Check git diff in both working directories.
Pick the more complete version as the base.
Manually merge the other session's unique changes.
Run the build and tests to verify.
Commit the merged result with a descriptive message.
If a session crashes mid-work:
Run git status and git diff to see uncommitted changes.
If the work is salvageable: git add . && git commit -m 'wip: session interrupted'
If starting fresh: git reset --hard HEAD && git clean -fd
Start a new session with recovery context describing what git diff showed.
1.5.7 Session Strategy by Phase
2. REPOSITORY STRUCTURE
Three separate repositories, each with its own CLAUDE.md file. The directory structures below are the canonical reference for file placement.
2.1 yfb-frontend (Next.js App)
yfb-frontend/
├── CLAUDE.md
├── SESSION_LOGS.md
├── feature-tracker.json          # Token-efficient project status (~200 tokens vs 2,000+ prose)
├── .claude/
│   ├── hooks.json                # Exit Code 2 guardrails (blocks cross-repo edits, any type, .env)
│   └── settings.json             # MCP CLI mode config (Supabase, GitHub, Vercel)
├── package.json
├── next.config.js
├── tailwind.config.ts
├── tsconfig.json                 # Strict mode — NON-NEGOTIABLE for AI-assisted dev
├── .env.local / .env.example
├── .github/
│   └── workflows/
│       └── ci.yml                # Lint + type-check + build + test on every PR
├── public/
│   ├── manifest.json, sw.js, icons/
│   └── locales/ (en.json, de.json, sv.json, da.json, no.json)
├── src/
│   ├── app/ (Next.js App Router)
│   │   ├── (auth)/ (login, signup, reset)
│   │   ├── (marketing)/ (landing, quiz/[step], quiz/results)
│   │   ├── (app)/ (dashboard, session, plan, coach, body, blood, nutrition, marketplace, settings)
│   │   ├── (admin)/ (users, quiz-editor, exercise-bank, videos, analytics)
│   │   ├── layout.tsx, globals.css
│   ├── components/ (ui/, quiz/, session/, coach/, charts/, marketplace/, shared/)
│   ├── hooks/, lib/ (supabase/, stripe/, i18n/, utils.ts)
│   ├── stores/ (Zustand), types/, styles/
└── tests/ (Playwright E2E + component)
└── docs/
    ├── PRD.md
    ├── TECH_GUIDE.md
    ├── AGENT_GUIDELINES.md
    └── ARCHITECTURE.md               # Architectural decisions + rationale
2.2 yfb-backend (Supabase + Edge Functions)
yfb-backend/
├── CLAUDE.md
├── SESSION_LOGS.md
├── feature-tracker.json              # Token-efficient project status
├── .claude/
│   ├── hooks.json                    # Exit Code 2 guardrails (blocks frontend/prompt edits, .env, test files)
│   └── settings.json                 # MCP CLI mode config (Supabase, GitHub)
├── .github/
│   └── workflows/
│       └── ci.yml                    # Deno type-check + migration validation on every PR
├── supabase/
│   ├── config.toml
│   ├── migrations/ (001_initial_schema.sql through 009+)
│   └── functions/ (generate-plan, coach-chat, coach-checkin, suggest-adjustment,
│       analyze-blood-panel, renpho-sync, stripe-webhook, stripe-checkout, quiz-resume)
├── scripts/ (seed-exercise-bank.ts, seed-quiz-questions.ts, export-anonymized.ts)
├── data/ (exercise-bank.json, quiz-questions.json, niche-messaging.json)
├── tests/
└── docs/
    ├── PRD.md
    ├── TECH_GUIDE.md
    ├── AGENT_GUIDELINES.md
    └── ARCHITECTURE.md               # Architectural decisions + rationale
2.3 yfb-ai-prompts (AI System Prompts & Templates)
yfb-ai-prompts/
├── CLAUDE.md
├── SESSION_LOGS.md
├── feature-tracker.json              # Token-efficient project status
├── changelog.md
├── .claude/
│   ├── hooks.json                    # Exit Code 2 guardrails (blocks application code edits)
│   └── settings.json                 # MCP CLI mode config (GitHub)
├── prompts/
│   ├── plan-generation/ (system-prompt.md, methodology.md, exercise-selection.md,
│   │   injury-protocols.md, output-schema.json, examples/*.json)
│   ├── coach-chat/ (system-prompt.md, personality.md, boundaries.md, check-in-templates/)
│   ├── supplement-analysis/ (system-prompt.md, marker-reference.md)
│   └── nutrition/ (system-prompt.md, meal-plan-rules.md)
├── tests/
│   ├── personas/                     # 5 starter personas (expand to 20+ through sprints)
│   │   ├── desk-worker-knee-pain.json
│   │   ├── advanced-lifter-plateau.json
│   │   ├── senior-beginner.json
│   │   ├── postpartum-return.json
│   │   └── martial-artist-shoulder.json
│   ├── plan-validation.ts
│   └── coach-behavior.ts
└── docs/
    ├── PRD.md
    ├── TECH_GUIDE.md
    ├── AGENT_GUIDELINES.md
    └── ARCHITECTURE.md               # Architectural decisions + rationale
3. CLAUDE.md SPECIFICATIONS (PER REPO)
Each repository has a CLAUDE.md file that Claude Code reads at session start. These are the complete, copy-paste-ready specifications.
3.1 yfb-frontend/CLAUDE.md
# Your Fitness Buddy — Frontend
## Project Overview
Next.js 14+ App Router application. PWA-enabled fitness platform.
Dark mode default. WCAG 2.1 AA compliant. i18n: EN, DE, SV, DA, NO.
Multi-agent project: you are the Frontend Agent. Stay in scope.
## Tech Stack
Next.js 14+ (App Router, Server Components default) | TypeScript (strict, no any)
Tailwind CSS + shadcn/ui | Zustand (client state) | Recharts (charts)
next-intl (i18n) | next-pwa + Workbox | Supabase JS client | Stripe JS
## Coding Rules
1. NEVER use 'any' type. Define proper interfaces in src/types/.
2. ALL components functional with hooks. No class components.
3. ALL user-facing strings via t('key'). NEVER hardcode strings.
4. EVERY interactive element: aria-label or visible text label.
5. EVERY image/icon: alt text.
6. Min touch target: 48x48px. Prefer 56x56px.
7. Server Components default. 'use client' only when hooks needed.
8. Files: PascalCase components, camelCase utils.
9. One component per file. Co-locate types in same file.
10. Props: [ComponentName]Props.
11. ALL colors from Tailwind theme tokens. NEVER hardcode hex.
12. Dark mode: use dark: prefix. Test BOTH themes.
13. Loading: skeleton components, never blank screens.
14. Errors: user-friendly message + retry. Never raw errors.
15. DO NOT modify src/lib/supabase/ without Backend coordination.
16. DO NOT write SQL or database logic.
17. DO NOT write or modify AI prompts.
## File Ownership
OWNS: src/app/, src/components/, src/hooks/, src/stores/,
      src/styles/, src/types/, public/locales/, tests/
READS (no modify): src/lib/supabase/, src/lib/stripe/
NEVER TOUCHES: Any file outside yfb-frontend/
## Session Protocol
1. Read this CLAUDE.md first, every session.
2. Check SESSION_LOGS.md for context from previous sessions.
3. Read feature-tracker.json for current project state and blockers.
4. Work within your file ownership scope.
5. End every session by updating feature-tracker.json with your changes.
6. Append session summary to SESSION_LOGS.md.
7. Document any API contracts consumed in your handoff notes.
3.2 yfb-backend/CLAUDE.md
# Your Fitness Buddy — Backend
## Project Overview
Supabase backend: PostgreSQL, Edge Functions (Deno/TS), RLS, webhooks.
ALL AI API calls happen here. Frontend never calls Claude directly.
Multi-agent project: you are the Backend Agent. Stay in scope.
## Tech Stack
Supabase (PostgreSQL 15+, Edge Functions, Auth, Storage, Realtime)
Deno/TypeScript (Edge Functions) | Anthropic Claude API | Stripe API
## Coding Rules
1. ALL DB changes via numbered SQL migrations. NEVER modify DB manually.
2. EVERY table: RLS policies. Default deny. Explicitly allow.
3. ALL API keys as env vars. NEVER hardcode secrets.
4. ALL user input validated + sanitized. Use Zod schemas.
5. ALL AI prompt content with user data: escape for prompt injection.
6. Edge Functions: one per endpoint. Max 50s timeout. Graceful errors.
7. Claude API: Sonnet for chat, Opus for plan gen. Always set max_tokens.
8. Stripe webhooks: verify signature. Idempotent handling.
9. Migration naming: NNN_verb_noun.sql
10. NEVER delete data. Soft deletes (deleted_at) or archive.
11. ALL timestamps UTC. Frontend handles timezone display.
12. DO NOT modify frontend code.
13. DO NOT modify AI prompt content. Read from yfb-ai-prompts.
14. Document API contracts in commit messages for Frontend Agent.
## File Ownership
OWNS: supabase/migrations/, supabase/functions/, scripts/, data/
READS (no modify): yfb-ai-prompts/ (for loading prompts)
NEVER TOUCHES: Any file outside yfb-backend/
## API Contract Documentation
Every new endpoint commit message MUST include:
- Method + path (POST /functions/v1/generate-plan)
- Request headers (Authorization: Bearer <token>)
- Request body schema (JSON)
- Response schema (JSON)
- Error codes (400, 401, 500 etc.)
This is how the Frontend Agent knows what to build against.
3.3 yfb-ai-prompts/CLAUDE.md
# Your Fitness Buddy — AI Prompts & Training Methodology
## Project Overview
ALL AI system prompts, training methodology, exercise selection rules,
coach personality, output schemas, and test personas.
This is the IP core of the product.
Multi-agent project: you are the AI Agent. Stay in scope.
## Rules
1. ALL prompts in Markdown (.md). Never embed prompts in code.
2. Use {{variable}} for dynamic injection ({{user_name}}, {{quiz_profile}}).
3. EVERY change documented in changelog.md with date + reason.
4. Output schemas (JSON) define EXACT structure. Edge Functions parse against these.
5. Test personas must cover edge cases: injuries + minimal equip, advanced athletes, seniors.
6. methodology.md is GROUND TRUTH. Plan gen prompts reference it, never contradict.
7. personality.md is GROUND TRUTH for coach voice. All coach comms must be consistent.
8. NEVER include real user data. Synthetic test data only.
9. DO NOT modify application code. This repo is prompts, docs, schemas, test data ONLY.
10. When changing output schemas, notify Backend Agent via SESSION_LOGS.md.
## File Ownership
OWNS: prompts/, tests/personas/, changelog.md
NEVER TOUCHES: Application code, database schema, frontend files
4. AGENT ROLE DEFINITIONS (EXPANDED)
Detailed activation prompts, responsibilities, boundaries, and output validation for each agent role.
4.1 Frontend Agent
Activation Prompt:
You are the Frontend Agent for Your Fitness Buddy. Read CLAUDE.md.
Check SESSION_LOGS.md for context from previous sessions.
Your job: build UI components, pages, and interactions for yfb-frontend.
Responsibilities:
React components, pages, App Router routing
Tailwind CSS styling (dark/light mode)
i18n strings in locale JSON files
Zustand state stores
Recharts data visualization wrappers
PWA manifest and service worker config
WCAG 2.1 AA accessibility compliance
Responsive design (mobile-first)
Playwright E2E tests and component tests
Boundaries (NEVER):
Write SQL or database migration files
Create or modify Edge Functions
Call Claude API directly (always through Edge Functions)
Write or modify AI system prompts
Handle server-side payment logic
Modify files in src/lib/supabase/ without Backend Agent coordination
Output Validation:
Every component compiles without TypeScript errors
Renders correctly in both dark and light mode
Passes axe-core accessibility checks
All strings extracted to locale files (no hardcoded text)
Touch targets minimum 48x48px
4.2 Backend Agent
Activation Prompt:
You are the Backend Agent for Your Fitness Buddy. Read CLAUDE.md.
Check SESSION_LOGS.md for context from previous sessions.
Your job: database schema, Edge Functions, and API logic for yfb-backend.
Responsibilities:
SQL migration files (numbered, sequential)
RLS policies (default deny, explicit allow)
Supabase Edge Functions (Deno/TypeScript)
Data validation with Zod schemas
Claude API integration (load prompts, call API, parse response)
Seed scripts for exercise bank and quiz questions
API contract documentation in commit messages
Boundaries (NEVER):
Write React components or modify CSS
Handle UI state or client-side logic
Write or modify AI prompt content (read from yfb-ai-prompts)
Expose API keys to frontend code
Output Validation:
Every migration applies cleanly to a fresh Supabase instance
Every Edge Function handles errors and returns proper HTTP status codes
All inputs validated with Zod before processing
API contracts documented in commit messages
4.3 AI Agent
Activation Prompt:
You are the AI Agent for Your Fitness Buddy. Read CLAUDE.md.
Check SESSION_LOGS.md for context from previous sessions.
Your job: system prompts, methodology, schemas, and coach behavior for yfb-ai-prompts.
Responsibilities:
System prompts for plan generation, coach chat, supplement analysis, nutrition
Training methodology documentation (periodization, exercise selection, injury protocols)
Output JSON schemas that Edge Functions parse against
Coach personality and communication style definition
Test personas covering 20+ edge case profiles
Prompt testing and iteration with validation
changelog.md updates for every prompt change
Boundaries (NEVER):
Write application code (JavaScript, TypeScript)
Modify database schema or migrations
Build UI components or modify styling
Include real user data in test files
Output Validation:
Every prompt generates valid JSON matching the output schema when tested with 3+ diverse personas
Coach responses stay in character and do not make medical claims
Edge case personas (multiple injuries, minimal equipment, seniors) produce safe, appropriate plans
4.4 Integration Agent
Activation Prompt:
You are the Integration Agent for Your Fitness Buddy. Read CLAUDE.md.
Your job: connect third-party services (Stripe, Renpho, wearables) to the backend.
Responsibilities: Third-party API client code, webhook handlers, data transformation, retry logic, error handling for external API failures.
Scope: Works within yfb-backend/supabase/functions/ only for integration-specific Edge Functions.
Boundaries: Does NOT modify database schema (requests migrations from Backend Agent), does NOT modify UI, does NOT write AI prompts.
4.5 Full-Stack Agent
Activation Prompt:
You are the Full-Stack Agent for Your Fitness Buddy. Read ALL CLAUDE.md files.
Your job: wire up a complete feature end-to-end across frontend, backend, and AI.
When to use: ONLY when building a feature that touches all layers simultaneously and coordination between separate agents would be too slow. Use sparingly.
Rules: Follow ALL conventions from ALL CLAUDE.md files. Backend CLAUDE.md takes precedence for data logic. Frontend CLAUDE.md takes precedence for UI logic.
4.6 DevOps Agent
Activation Prompt:
You are the DevOps Agent for Your Fitness Buddy.
Your job: deployment, CI/CD, monitoring, and infrastructure.
Responsibilities: Vercel config, Supabase CLI setup, GitHub Actions CI, environment variable management, PWA service worker, Sentry error tracking, PostHog analytics, AI cost monitoring.
5. ENVIRONMENT VARIABLES & SECRETS
Unchanged from TechGuide v1.0. Key rule: NEVER commit .env files. ALL secret API calls go through Edge Functions. NEXT_PUBLIC_ prefix = exposed to browser.
6. DATABASE SCHEMA & MIGRATION STRATEGY
Unchanged from TechGuide v1.0. Backend Agent owns all migrations. Numbered sequentially. Never modify applied migrations. RLS on every table.
7. AI PROMPT ENGINEERING (SYSTEM PROMPTS)
Unchanged from TechGuide v1.0. Plan generation uses multi-document composition (system-prompt.md + methodology.md + exercise-selection.md + injury-protocols.md + output-schema.json). Claude Opus for plan gen, Sonnet for chat. Prompts versioned in changelog.md.
8. CODING CONVENTIONS & STANDARDS
Unchanged from TechGuide v1.0. See individual CLAUDE.md files (Section 3) for repo-specific conventions.
9. PROJECT SETUP GUIDE (DAY 1)
Updated to reflect three-repo structure with v2.1 agent infrastructure:
Create three GitHub repos: yfb-frontend, yfb-backend, yfb-ai-prompts. Initialize each with:
  - CLAUDE.md (from Section 3)
  - SESSION_LOGS.md (empty template)
  - feature-tracker.json (sprint-mapped status tracker — agents read at session start, update at session end)
  - .claude/hooks.json (Exit Code 2 guardrails — block cross-repo file edits at the tool level)
  - .claude/settings.json (MCP CLI mode configuration — saves context window budget)
  - docs/ARCHITECTURE.md (architectural decisions + rationale — shared across all 3 repos)
Set up Supabase project (supabase.com). Install CLI. Link project.
Set up Next.js project (create-next-app with TypeScript, Tailwind, App Router). Install all dependencies per CLAUDE.md. Verify tsconfig.json has ALL strict mode flags enabled (NON-NEGOTIABLE for AI-assisted development).
Set up Stripe (create products: Free, Pro $19.99/mo, Business $49.99/mo). Configure webhook to yfb-backend.
Set up Anthropic API key in Supabase Edge Function secrets.
Backend Agent: Write initial migrations (001_initial_schema.sql through 006_rls_policies.sql). Apply with supabase db push.
Connect yfb-frontend to Vercel. Set environment variables. Verify deployment.
Add .github/workflows/ci.yml to yfb-frontend (lint + type-check + build + test on PR) and yfb-backend (Deno type-check + migration validation on PR). Verify CI passes on initial commit.
10. MVP TASK BREAKDOWN (UPDATED WITH SESSION STRATEGY)
Each sprint task now includes the recommended agent and session strategy.
Sprint 1 (Week 1-2): Foundation
Sprint 2 (Week 3-4): Quiz Funnel
Sprint 3 (Week 5-6): AI Plan Generation
Sprint 4 (Week 7-8): Workout Tracker
Same pattern: Backend Agent builds tables + Edge Functions, AI Agent writes coach prompts, Frontend Agent builds session logger UI.
Sprint 5 (Week 9-10): Payments + Polish + i18n
Integration Agent handles Stripe webhook + checkout. Frontend Agent handles UI. Translations can run in parallel (different files, no conflicts).
Sprint 6 (Week 11-12): Testing + Launch Prep
Full-Stack Agent for integration testing. DevOps Agent for production deployment checklist.
Total: ~310 hours + 20% buffer = ~370 hours across 12 weeks.
11. TESTING & QA PROTOCOL
Unchanged from TechGuide v1.0. AI plan validation with 20+ persona test suite. Quiz logic automated tests. Playwright E2E for critical flows. axe-core accessibility scans in CI.
12. DEPLOYMENT PIPELINE
Updated for multi-repo with automated CI:
yfb-frontend: Auto-deploy to Vercel from main branch on every push. CI via `.github/workflows/ci.yml` runs lint → type-check → build → unit tests on every PR. PRs that fail CI cannot merge.
yfb-backend: Manual deploy via supabase db push (migrations) and supabase functions deploy (Edge Functions). Never auto-deploy backend. CI via `.github/workflows/ci.yml` runs Deno type-check on all Edge Functions + validates migration numbering + checks RLS policies on every PR.
yfb-ai-prompts: No direct deployment. Prompts are bundled into Edge Functions at backend deploy time. No CI workflow (content validation is manual via test personas).
CI/CD: GitHub Actions on frontend and backend repos. On PR: lint, type-check, build, test. On merge to main: deploy (frontend only auto, backend manual). Agent guardrails (`.claude/hooks.json`) prevent cross-repo file edits before code even reaches CI.
13. HANDOFF CHECKLIST (PER AGENT SESSION)
Updated checklist for multi-agent workflow. Complete ALL items before closing ANY Claude Code session:
All changes committed with descriptive messages.
All new files follow repo naming conventions.
No TypeScript errors (npm run build / deno check).
No ESLint errors.
All tests passing.
feature-tracker.json updated (status, blockers, contracts).
i18n: No hardcoded strings (Frontend Agent).
Accessibility: axe-core passes (Frontend Agent).
RLS policies on all new tables (Backend Agent).
Environment variables documented (Backend Agent).
Changes pushed to remote.
API contracts documented in commit message if creating endpoints.
Session summary appended to SESSION_LOGS.md.
Next session strategy documented (sequential/parallel).
No files modified outside agent's ownership scope.
