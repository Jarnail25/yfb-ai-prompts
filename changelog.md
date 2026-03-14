# AI Prompts Changelog

All prompt changes are logged here with date, what changed, and why.
AI Agent: update this file with EVERY prompt modification.

---

## 2026-03-16 — v4.1 (Few-Shot Plan Examples)

- Added `prompts/plan-generation/examples/README.md` — documents usage pattern for Edge Function injection
- Added `examples/example-01-commercial-gym-intermediate.md` — complete Phase 1 Session A (all 6 blocks), Phase 2/3 as progression deltas, warm_ups + deload_protocol + readiness_assessment. Baseline for no-injury commercial gym profile.
- Added `examples/example-02-home-gym-beginner-lower-back.md` — home gym equipment substitutions (no barbell, DBs + bands), lower back injury protocol (McGill Big 3 mandatory, no bilateral heavy hinging, BW back extension only P1). Shows beginner load prescription and Nordic regression.
- Added `examples/example-03-advanced-shoulder-impingement.md` — anterior shoulder impingement substitutions (landmine press replaces OHP, face pull mandatory every warm-up, no upright row, pull-dominant skew). Includes substitution reference table.
- Feature tracker updated: plan_few_shot_examples → complete

---

## 2026-02-08 — v1.0 (Initial Bootstrap)
- Created repository structure with multi-agent orchestration
- Added CLAUDE.md with AI Agent instructions (v2 — multi-agent aware)
- Added PRD v2.0 and TechGuide v2.0 reference docs
- Added SESSION_LOGS.md for handoff protocol
- Prompt files to be created in Sprint 3 (Weeks 5-6)
- Empty directory structure for: plan-generation, coach-chat, supplement-analysis, nutrition

---

## 2026-02-08 — v1.1 (Sprint 3: Plan Generation Prompts)
- Created `prompts/plan-generation/system-prompt.md` — Master system prompt for AI plan generation. Defines inputs (full quiz profile JSON), safety rules, output requirements. References methodology, exercise-selection, and injury-protocols as composed documents.
- Created `prompts/plan-generation/methodology.md` — GROUND TRUTH training methodology. 3-phase periodization (Foundation → Accumulation → Realization), A/B/C/D block session structure, Cressey-influenced warm-up, pull:push 3:2 ratio, lunge-dominant lower body, Nordic curls every session, isometric/end-range/core progressions across phases, deload every 4th week, tempo and RPE guidelines.
- Created `prompts/plan-generation/exercise-selection.md` — Equipment mapping, experience level adjustments (beginner/intermediate/advanced), body type and anthropometry rules (tall users, desk workers, 40+, 55+), goal-based exercise priority, session type exercise pools (A/B/C), substitution rules.
- Created `prompts/plan-generation/injury-protocols.md` — Protocols for knee (ACL, MCL/LCL, meniscus, patellofemoral), shoulder (impingement, rotator cuff), lower back (general, disc, post-surgery), hip (FAI), ankle, neck, elbow/wrist. Includes severity scale, medical override rules, multiple injury handling, movement screening proxy adjustments.
- Created `prompts/plan-generation/output-schema.json` — Full JSON Schema (draft 2020-12) defining the plan output structure. Covers: plan metadata, phases, sessions (with week/day/type/deload), warm-up (foam rolling + movement prep + neural activation), blocks (A/B/C/D), exercises (name, sets, reps, tempo, RPE, load, coaching cues, progression notes, equipment, muscle groups), plan notes.
- Created `tests/personas/beginner-knee-injury-home-gym.json` — Test persona: 42F, beginner, ACL post-surgery, home gym (DB + bands), desk worker, fat loss goal. Tests injury protocol, beginner limits, minimal equipment, posture corrections.
- Created `tests/personas/advanced-martial-artist-full-gym.json` — Test persona: 28M, advanced, competitive BJJ, full gym, mild shoulder impingement. Tests sport-specific programming, rotational emphasis, competition peaking, shoulder protocol.
- Created `tests/personas/senior-multiple-injuries-minimal-equip.json` — Test persona: 61M, deconditioned senior, disc bulge + knee OA, kettlebells + bands only. Tests 55+ adjustments, multiple injury handling, conservative programming, longevity goal.

---

## 2026-03-15 — v4.0 (Coach Prompts + Backend v3.1 Unblock)

### Coach Chat Prompts (Sprint 4 — all new)
- **`prompts/coach-chat/personality.md`** — GROUND TRUTH for coach voice. Direct but warm persona, evidence-based, no filler affirmations. Tone-by-situation table (PR/PR miss/injury/complex programming/off-topic). Language style guide (Australian English, no motivational clichés). 6 non-negotiable character rules.
- **`prompts/coach-chat/system-prompt.md`** — Full coach system prompt. Embeds 6-block methodology, periodization phases, movement priorities (pull:push 3:2, lunge-dominant, Nordic curls). Response rules: 2-4 paragraphs default, injury → physio referral, readiness ≤3 → reduce intensity 10-15%. Implementation notes for backend maintainers.
- **`prompts/coach-chat/boundaries.md`** — Explicit coach scope. Can: training, recovery, general nutrition principles, injury management (not diagnosis). Cannot: diagnose, prescribe supplements/meds, create meal plans, write new training plans. Grey-area handling table for 6 common edge cases.
- **`prompts/coach-chat/check-in-templates/weekly-checkin.md`** — Weekly check-in system prompt template. Main template + 3 variants: missed sessions, deload week reminder, phase transition. Includes example output for testing.

### Backend Unblock
- generate-plan Edge Function rewritten to v3.1 schema (deployed as version 4, ACTIVE 2026-03-15). Blocking blocker in feature-tracker cleared. Session templates, 6 blocks, nested exercises, exercise_bank_ref, deload halving all implemented.

### Feature Tracker
- `coach_personality`: not_started → complete
- `coach_system_prompt`: not_started → complete
- `coach_checkin_templates`: not_started → complete
- `test_personas`: in_progress → complete (8 personas exist, target met)
- Cleared blocking blocker for `plan_output_schema`

---

## 2026-03-01 — v3.1 (Training Methodology Integration Update)

Bridges the gap between the battle-tested training methodology (validated through the 12-Week Training Tracker build) and the AI plan generation system. Adds structured data, schemas, and rules the AI engine needs to generate plans at hand-built quality.

### New Files Added to `prompts/plan-generation/`
- **`block-taxonomy.md`** — Complete 6-block (A-F) session architecture reference. Defines block purpose, exercise counts, phase progressions, timing, and mandatory inclusions for each block. Documents Session D's unique per-phase structure. Authoritative reference — overrides other docs on block structure.
- **`plan-generation-constraints.md`** — 15 non-negotiable hard rules for AI plan generation: structural constraints (SC-1 to SC-5), periodization constraints (PC-1 to PC-5), progression constraints (PRG-1 to PRG-7), exercise selection constraints (ES-1 to ES-6), warm-up constraints (WU-1 to WU-2), plus 15-point self-validation checklist.
- **`exercise-bank-schema.json`** — 100+ exercises categorized by movement pattern (squat, hinge, vertical pull, horizontal pull, pressing, rotation, isometric, core, neck, accessories, plyometrics). Each exercise tagged with block assignment, session specificity, phase applicability, equipment requirements, and substitutions. Includes equipment mapping profiles (home_gym_full, home_gym_minimal, commercial_gym, bodyweight_only).
- **`progression-rules.json`** — Structured per-block, per-phase progression data. Defines sets, reps, tempo, RPE, rest, weekly load increase, and training quality for every block across all 3 phases plus deload. Includes warm-up progressions per phase.

### Updated Files
- **`output-schema.json`** — REPLACED with v3.1 schema. Major changes: blocks now A-F (was A-D), added `validation_checks` object (12 self-check booleans), added `warm_ups` (phase-specific protocols), added `deload_protocol`, added `readiness_assessment`, added per-exercise `weekly_progression` and `substitutions` arrays, added `movement_category` enum, added `pull_push_count` per session.

### PRD Patches (applied to `docs/PRD.md`)
- **Section 2.2** — Filled empty "Competitive Differentiation" section with 6 differentiators and competitive landscape table
- **Section 5.2.1-5.2.4** — Added block taxonomy, accessory distribution rule, E-block session specificity, mandatory session inclusions
- **Section 5.3** — Added steps 6-8 (validation, structured output, re-validation) and constraint files reference table
- **Section 19.1** — Filled empty "Brand Identity Requirements" with color palette, typography, UI personality, coach visual persona
- **Section 23.1** — Filled empty "Error Handling & Resilience" with Claude API, Stripe, Supabase failure scenarios and graceful degradation priorities
- **Section 23.3** — Filled empty "Performance Targets" with Web Vitals budgets, feature-specific targets, bundle size budgets, CI enforcement
