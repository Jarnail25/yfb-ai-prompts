# Your Fitness Buddy — AI Prompts & Training Methodology

## Project Overview
ALL AI system prompts, training methodology, exercise selection rules,
coach personality, output schemas, and test personas.
This is the IP core of the product.
Multi-agent project: you are the AI Agent. Stay in scope.

**Read `docs/PRD.md` and `docs/TECH_GUIDE.md` for full product and technical context.**

## Rules
1. ALL prompts in Markdown (`.md`). Never embed prompts in code.
2. Use `{{variable}}` for dynamic injection (`{{user_name}}`, `{{quiz_profile}}`).
3. EVERY change documented in `changelog.md` with date + reason.
4. Output schemas (JSON) define EXACT structure. Edge Functions parse against these.
5. Test personas must cover edge cases: injuries + minimal equip, advanced athletes, seniors, postpartum.
6. `prompts/plan-generation/methodology.md` is **GROUND TRUTH**. Plan gen prompts reference it, never contradict.
7. `prompts/coach-chat/personality.md` is **GROUND TRUTH** for coach voice. All coach comms must be consistent.
8. NEVER include real user data. Synthetic test data only.
9. DO NOT modify application code. This repo is prompts, docs, schemas, test data ONLY.
10. When changing output schemas, notify Backend Agent via SESSION_LOGS.md.

## File Ownership
- **OWNS:** `prompts/`, `tests/personas/`, `changelog.md`
- **NEVER TOUCHES:** Application code, database schema, frontend files

## Folder Structure
```
yfb-ai-prompts/
├── CLAUDE.md
├── SESSION_LOGS.md
├── changelog.md
├── prompts/
│   ├── plan-generation/
│   │   ├── system-prompt.md          # Master system prompt
│   │   ├── methodology.md            # Training philosophy (GROUND TRUTH)
│   │   ├── exercise-selection.md     # Exercise bank rules
│   │   ├── injury-protocols.md       # Injury-specific modifications
│   │   ├── output-schema.json        # Required JSON structure
│   │   └── examples/                 # Few-shot examples
│   ├── coach-chat/
│   │   ├── system-prompt.md          # Coach behavior rules
│   │   ├── personality.md            # Voice, tone, style (GROUND TRUTH)
│   │   ├── boundaries.md             # Can/cannot do
│   │   └── check-in-templates/       # Automated message templates
│   ├── supplement-analysis/
│   │   ├── system-prompt.md
│   │   └── marker-reference.md       # Blood marker ranges
│   └── nutrition/
│       ├── system-prompt.md
│       └── meal-plan-rules.md
├── tests/
│   ├── personas/                     # 20+ test persona JSON files
│   ├── plan-validation.ts            # Automated safety checks
│   └── coach-behavior.ts             # Coach response quality tests
└── docs/
    ├── PRD.md
    └── TECH_GUIDE.md
```

## Prompt Composition (How Prompts Are Assembled at Runtime)

### Plan Generation
```
SYSTEM = system-prompt.md + methodology.md + exercise-selection.md + injury-protocols.md
USER = { quiz_profile_json } + "Generate a complete periodized training plan."
OUTPUT = Must match output-schema.json
MODEL = Claude Opus | Temperature: 0.3 | Max tokens: 12000
```

### Coach Chat
```
SYSTEM = system-prompt.md + personality.md + boundaries.md + {user_profile} + {plan_state} + {last_5_sessions} + {body_comp_trends}
USER = {user_message}
MODEL = Claude Sonnet | Temperature: 0.5 | Max tokens: 500
```

### Supplement Analysis
```
SYSTEM = system-prompt.md + marker-reference.md + {user_profile} + {training_phase}
USER = {blood_panel_data}
MODEL = Claude Sonnet | Temperature: 0.2 | Max tokens: 2000
```

## Training Methodology Summary (for quick reference)
- **Periodization:** 3-phase (Foundation → Accumulation → Realization), 8-12 weeks
- **Sessions:** Full-body, A/B/C/D block format (Primary → Secondary+Rotation → Isometric+End-Range → Core)
- **Rotation:** A (sagittal), B (frontal/rotational), C (posterior chain) — all 3 weekly
- **Pull:Push ratio:** 3:2 minimum
- **Lower body:** Lunge/split-squat dominant (no heavy back squats as default)
- **Warm-up:** Cressey-influenced (foam roll → movement prep → neural activation)
- **Isometrics:** Yielding → Overcoming → Functional → Reactive across phases
- **End-range:** PAILs/RAILs → loaded stretches → dynamic end-range across phases
- **Nordics:** Every session (eccentric → full range → reactive across phases)
- **Deload:** Every 4th week (40-50% volume reduction)

## Session Protocol
1. Read this CLAUDE.md first, every session.
2. Check SESSION_LOGS.md for context from previous sessions.
3. Work within your file ownership scope.
4. End every session by appending to SESSION_LOGS.md.
5. When changing output schemas, note in handoff for Backend Agent.

## Session End Checklist
1. ✅ All prompt changes logged in `changelog.md`
2. ✅ Output schemas updated if prompt output structure changed
3. ✅ Tested against 3+ diverse personas
4. ✅ Coach responses stay in character and within boundaries
5. ✅ No medical claims or diagnoses in any prompt output
6. ✅ No real user data in any file
7. ✅ Session summary appended to SESSION_LOGS.md
8. ✅ No files modified outside ownership scope
