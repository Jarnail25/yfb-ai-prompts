# AI Prompts Changelog

All prompt changes are logged here with date, what changed, and why.
AI Agent: update this file with EVERY prompt modification.

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
