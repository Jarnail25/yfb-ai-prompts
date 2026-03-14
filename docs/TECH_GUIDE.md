# TECHNICAL IMPLEMENTATION GUIDE
# Your Fitness Buddy
Version 3.0 | March 2026
Personal fitness tool — solo development with Claude Code

---

1. DEVELOPMENT STRATEGY

1.1 Philosophy
This is a personal tool built by one developer using Claude Code. The project is split across three repos with clear boundaries — not for multi-agent coordination, but to keep context clean and concerns separated.

Each repo has its own CLAUDE.md file that defines what's in scope, coding rules, and how the piece fits the whole.

1.2 The Three Repositories

| Repo | Purpose | Primary Tech |
|------|---------|--------------|
| `yfb-frontend` | UI, UX, PWA | Next.js, TypeScript, Tailwind, Supabase JS |
| `yfb-backend` | DB schema, Edge Functions, AI calls | Supabase, Deno/TS, Zod |
| `yfb-ai-prompts` | System prompts, methodology, output schemas | Markdown, JSON |

1.3 Critical Rules
- ALL AI API calls happen in Edge Functions. Frontend never calls Claude directly.
- Shared TypeScript types live in `yfb-frontend/src/types/` (canonical source). Backend uses equivalent Zod schemas.
- TypeScript strict mode is NON-NEGOTIABLE.
- `methodology.md` is GROUND TRUTH. Nothing contradicts it.

1.4 Session Protocol
Every session:
1. Read the repo's CLAUDE.md.
2. Read `feature-tracker.json` for current project state.
3. Build the feature.
4. Update `feature-tracker.json` at session end.

---

2. REPOSITORY STRUCTURE

2.1 yfb-frontend

```
yfb-frontend/
├── CLAUDE.md
├── feature-tracker.json
├── package.json
├── next.config.ts
├── tailwind.config.ts
├── tsconfig.json
├── public/
│   └── manifest.json, sw.js, icons/
└── src/
    ├── app/
    │   ├── (auth)/          # login, signup, reset
    │   ├── (app)/           # dashboard, session, plan, coach, body, blood, settings
    │   ├── layout.tsx
    │   └── globals.css
    ├── components/
    │   ├── ui/              # shadcn/ui base
    │   ├── session/         # session tracker
    │   ├── coach/           # chat UI
    │   ├── charts/          # Recharts wrappers
    │   └── shared/          # layout, nav, modals
    ├── hooks/
    ├── lib/
    │   ├── supabase/        # client config
    │   └── utils.ts
    ├── stores/              # Zustand
    ├── types/               # TypeScript types (canonical source)
    └── styles/              # theme tokens
```

2.2 yfb-backend

```
yfb-backend/
├── CLAUDE.md
├── feature-tracker.json
├── supabase/
│   ├── config.toml
│   ├── migrations/
│   │   ├── 001_initial_schema.sql
│   │   ├── 002_create_quiz_tables.sql
│   │   ├── 003_create_training_tables.sql
│   │   └── ...
│   └── functions/
│       ├── generate-plan/index.ts
│       ├── coach-chat/index.ts
│       ├── coach-checkin/index.ts
│       ├── suggest-adjustment/index.ts
│       ├── analyze-blood-panel/index.ts
│       ├── renpho-sync/index.ts
│       └── quiz-resume/index.ts
├── scripts/
│   ├── seed-exercise-bank.ts
│   └── seed-quiz-questions.ts
└── data/
    ├── exercise-bank.json
    └── quiz-questions.json
```

2.3 yfb-ai-prompts

```
yfb-ai-prompts/
├── CLAUDE.md
├── changelog.md
├── feature-tracker.json
├── prompts/
│   ├── plan-generation/
│   │   ├── system-prompt.md
│   │   ├── methodology.md         # GROUND TRUTH
│   │   ├── exercise-selection.md
│   │   ├── injury-protocols.md
│   │   ├── block-taxonomy.md
│   │   ├── plan-generation-constraints.md
│   │   ├── output-schema.json
│   │   ├── progression-rules.json
│   │   ├── exercise-bank-schema.json
│   │   └── examples/
│   └── coach-chat/
│       ├── system-prompt.md
│       ├── personality.md         # GROUND TRUTH for coach voice
│       ├── boundaries.md
│       └── check-in-templates/
├── tests/
│   ├── personas/                  # 8+ test persona JSON files
│   ├── plan-validation.ts
│   └── coach-behavior.ts
└── docs/
    ├── PRD.md
    ├── TECH_GUIDE.md
    └── ARCHITECTURE.md
```

---

3. CLAUDE.md SPECS (SUMMARY)

Each CLAUDE.md defines the scope for that repo. Full specs live in each repo's CLAUDE.md. Key boundaries:

- `yfb-frontend`: Owns `src/app/`, `src/components/`, `src/hooks/`, `src/stores/`, `src/types/`. Never writes SQL or AI prompts.
- `yfb-backend`: Owns `supabase/migrations/`, `supabase/functions/`, `scripts/`, `data/`. Never writes React or AI prompts.
- `yfb-ai-prompts`: Owns `prompts/`, `tests/personas/`, `changelog.md`. Never writes application code.

---

5. ENVIRONMENT VARIABLES & SECRETS

All secrets in local env files (never committed). Reference via `EnvironmentFile=` in systemd or `--env-file` in Docker.

**yfb-frontend** (local env file):
- `NEXT_PUBLIC_SUPABASE_URL`
- `NEXT_PUBLIC_SUPABASE_ANON_KEY`

**yfb-backend** (Supabase Secrets via dashboard or `supabase secrets set`):
- `ANTHROPIC_API_KEY`
- `RENPHO_API_KEY`
- `RESEND_API_KEY`
- `APP_URL`

---

6. DATABASE SCHEMA & MIGRATION STRATEGY

All schema changes via numbered SQL migrations in `yfb-backend/supabase/migrations/`. Never modify applied migrations — create a new one.

Naming: `NNN_verb_noun.sql` (e.g., `004_add_blood_panel_tables.sql`)

Applied migrations (as of Sprint 2):
- `001_initial_schema.sql` — profiles, quiz_responses, moddatetime trigger
- `002_create_quiz_tables.sql` — quiz_categories, quiz_questions, exercise_bank + RLS
- `003_create_training_tables.sql` — training_plans, plan_phases, plan_sessions, plan_session_exercises, session_logs, set_logs + RLS

Key conventions:
- Every table: `id` (uuid PK), `created_at`, `updated_at` (timestamptz)
- RLS on every table. Default deny. Explicitly allow.
- Soft deletes (`deleted_at`). Never hard-delete user data.
- All timestamps UTC.

---

7. AI PROMPT ENGINEERING

**Plan Generation:**
```
SYSTEM = system-prompt.md + methodology.md + exercise-selection.md + injury-protocols.md
         + block-taxonomy.md + plan-generation-constraints.md
USER = { quiz_profile_json } + "Generate a complete periodized training plan."
OUTPUT = Must match output-schema.json (v3.1)
MODEL = Claude Opus | Temperature: 0.3 | Max tokens: 16000
```

**Coach Chat:**
```
SYSTEM = system-prompt.md + personality.md + boundaries.md
         + {user_profile} + {plan_state} + {last_5_sessions}
USER = {user_message}
MODEL = Claude Sonnet | Temperature: 0.5 | Max tokens: 500
```

**Supplement Analysis:**
```
SYSTEM = system-prompt.md + marker-reference.md + {user_profile} + {training_phase}
USER = {blood_panel_data}
MODEL = Claude Sonnet | Temperature: 0.2 | Max tokens: 2000
```

Prompt versioning: Every change logged in `changelog.md` with date + reason.

---

10. SPRINT PLAN

| Sprint | Status | Goal |
|--------|--------|------|
| Sprint 1 | complete | Foundation — Next.js, Supabase schema, auth UI, quiz seeded, quiz-resume Edge Function, 95-exercise bank |
| Sprint 2 | complete | AI Plan Generation + coaching — generate-plan, coach-chat, coach-checkin Edge Functions |
| Sprint 3 | next | Frontend plan viewer — display generated plan, phase/session navigation |
| Sprint 4 | planned | Session tracker — set logging, rest timer, offline mode, Zustand store |
| Sprint 5 | planned | Dashboard + body comp — Whoop-style UI, Renpho integration, trend charts |
| Sprint 6 | planned | Blood panel + supplement protocol UI |
| Sprint 7 | planned | Polish — notifications, plan versioning, settings, accessibility audit |

---

11. TESTING PROTOCOL

AI plan validation personas (8+ profiles):
- beginner-knee-injury-home-gym
- advanced-martial-artist-full-gym
- senior-multiple-injuries-minimal-equip
- desk-worker-fat-loss
- postpartum-return
- 40plus-hormonal-full-gym
- competitive-sport-strength-focus
- complete-beginner-commercial-gym

Automated checks per plan: no contraindicated exercises, correct phase structure, pull-to-push ratio ≥ 3:2, deload week present.
Coach behavior tests: responses stay in character, no medical claims, in-boundary topics only.

---

12. DEPLOYMENT

- **Frontend:** Next.js, self-hosted or Supabase hosting. No Vercel dependency.
- **Backend:** Supabase project (yxdmutjfxbqwjvtrzfey, us-west-2). Migrations via `supabase db push`. Functions via `supabase functions deploy`.
- **Prompts:** Bundled into Edge Functions at deploy time (not fetched at runtime).
- **Local dev:** `supabase start` gives full Postgres + Auth + Functions stack locally.

---

13. SESSION CHECKLIST

Before ending any session:
- All changes committed with descriptive message
- No TypeScript errors (`npm run build` or `deno check`)
- `feature-tracker.json` updated (status, blockers)
- No hardcoded secrets
- RLS policies on all new tables (backend sessions)
- API contracts documented in commit message if creating endpoints
