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
