# Session Logs — yfb-ai-prompts

Append to this file at the end of EVERY Claude Code session on this repo.
The next agent reads this for context.

---

<!-- 
## Session [N]: [DATE] - [AGENT ROLE]
Duration: [X]h | Commits: [hashes] | Branch: main

### Completed
- [What was built/fixed, files created/modified]

### Interface Contracts
- [METHOD] /path — Request: { schema } → Response: { schema }
- Component: Name — Props: { interface }

### Known Issues
- [Bugs found, workarounds, tech debt created]

### Next Session
- Agent: [recommended role]
- Strategy: Sequential after this / Can parallel with [X]
- Tasks: 1) [task] 2) [task] 3) [task]

### Handoff Notes
- [Gotchas, why decisions were made, what next agent needs to know]
-->

## Session 1: 2026-02-08 - AI Agent

Commits: TBD | Branch: claude/bootstrap-project-ALpMC

### Completed
- Reset branch to match user's updated `main` (PRD v2.0, TECH_GUIDE v2.0, AGENT_GUIDELINES, new CLAUDE.md)
- Previous Sprint 1 work (generic schemas, prompts, scripts) was discarded — did not match PRD/TECH_GUIDE vision
- Created all Sprint 3 plan-generation prompt files:
  - `prompts/plan-generation/system-prompt.md` — Master system prompt
  - `prompts/plan-generation/methodology.md` — GROUND TRUTH training methodology
  - `prompts/plan-generation/exercise-selection.md` — Equipment, experience, body type, goal-based rules
  - `prompts/plan-generation/injury-protocols.md` — Full injury protocol library (knee, shoulder, back, hip, ankle, neck, elbow/wrist, multiple injuries)
  - `prompts/plan-generation/output-schema.json` — JSON Schema for plan output (phases → sessions → warm-up + blocks → exercises)
- Created 3 test personas in `tests/personas/`:
  - `beginner-knee-injury-home-gym.json` — 42F, ACL post-surgery, DB + bands, desk worker
  - `advanced-martial-artist-full-gym.json` — 28M, competitive BJJ, full gym, shoulder impingement
  - `senior-multiple-injuries-minimal-equip.json` — 61M, disc bulge + knee OA, kettlebells + bands
- Updated `changelog.md` with all changes

### Interface Contracts
- `output-schema.json` defines the plan generation output contract. Backend Agent's `generate-plan` Edge Function must parse against this schema with Zod.
- Schema structure: `{ plan_name, phases[{ sessions[{ warm_up, blocks[{ exercises[] }] }] }], plan_notes }`

### Known Issues
- No few-shot examples yet in `prompts/plan-generation/examples/` — would improve generation quality but requires generating a full sample plan
- Coach chat, supplement analysis, and nutrition prompts not yet written (Sprint 4+ scope)
- No automated plan validation script yet (`tests/plan-validation.ts` and `tests/coach-behavior.ts` referenced in CLAUDE.md but not created)

### Next Session
- Agent: AI Agent
- Strategy: Sequential
- Tasks:
  1) Write `prompts/coach-chat/` prompts (system-prompt.md, personality.md, boundaries.md, check-in templates)
  2) Write `prompts/supplement-analysis/` prompts (system-prompt.md, marker-reference.md)
  3) Write `prompts/nutrition/` prompts (system-prompt.md, meal-plan-rules.md)
  4) Add few-shot examples to `prompts/plan-generation/examples/`
  5) Create additional test personas to reach 20+ coverage

### Handoff Notes
- `methodology.md` is the GROUND TRUTH — all plan generation prompts reference it. If the founder updates training philosophy, update this file FIRST, then cascade.
- Injury protocols cover the major quiz categories (5, 10, 11 from PRD). Multiple injury rule: when protocols conflict, use the MORE CONSERVATIVE option.
- Output schema is designed to be Zod-parseable. Backend Agent should generate Zod schema from this JSON Schema.
- Test personas include `expected_plan_properties` — these define what automated validation should check for each persona.
