# Your Fitness Buddy — AI Prompts & Training Methodology

## Project Overview
ALL AI system prompts, training methodology, exercise selection rules,
coach personality, output schemas, and test personas.
This is the IP core of the product — a personal fitness tool for Jarnail.

**Read `docs/PRD.md` for full product context.**
**Read `docs/TECH_GUIDE.md` for technical context.**
**Read `docs/ARCHITECTURE.md` for architectural decisions.**

## Rules
1. ALL prompts in Markdown (`.md`). Never embed prompts in code.
2. Use `{{variable}}` for dynamic injection (`{{user_name}}`, `{{quiz_profile}}`).
3. EVERY change documented in `changelog.md` with date + reason.
4. Output schemas (JSON) define EXACT structure. Edge Functions parse against these.
5. Test personas must cover edge cases: injuries + minimal equip, advanced athletes, seniors.
6. `prompts/plan-generation/methodology.md` is **GROUND TRUTH**. Plan gen prompts reference it, never contradict.
7. `prompts/coach-chat/personality.md` is **GROUND TRUTH** for coach voice. All coach comms must be consistent.
8. NEVER include real user data. Synthetic test data only.
9. DO NOT modify application code. This repo is prompts, docs, schemas, test data ONLY.
10. When changing output schemas, log in `changelog.md` and note that backend Edge Functions must be updated.

## File Ownership
- **OWNS:** `prompts/`, `tests/personas/`, `changelog.md`
- **NEVER TOUCHES:** Application code, database schema, frontend files

## Folder Structure
```
yfb-ai-prompts/
├── CLAUDE.md
├── changelog.md
├── feature-tracker.json
├── prompts/
│   ├── plan-generation/
│   │   ├── system-prompt.md          # Master system prompt
│   │   ├── methodology.md            # Training philosophy (GROUND TRUTH)
│   │   ├── exercise-selection.md     # Exercise bank rules
│   │   ├── injury-protocols.md       # Injury-specific modifications
│   │   ├── block-taxonomy.md         # 6-block session structure (v3.1)
│   │   ├── plan-generation-constraints.md  # 15-point validation checklist
│   │   ├── output-schema.json        # Required JSON structure (v3.1)
│   │   ├── progression-rules.json    # Per-block, per-phase progression
│   │   ├── exercise-bank-schema.json # Exercise database schema
│   │   └── examples/                 # Few-shot examples
│   └── coach-chat/
│       ├── system-prompt.md          # Coach behavior rules
│       ├── personality.md            # Voice, tone, style (GROUND TRUTH)
│       ├── boundaries.md             # Can/cannot do
│       └── check-in-templates/       # Automated message templates
├── tests/
│   ├── personas/                     # 8+ test persona JSON files
│   ├── plan-validation.ts            # Automated safety checks
│   └── coach-behavior.ts             # Coach response quality tests
└── docs/
    ├── PRD.md
    ├── TECH_GUIDE.md
    ├── ARCHITECTURE.md
    └── AGENT_GUIDELINES.md

## Training Methodology Summary (quick reference)
- **Periodization:** 3-phase (Foundation → Accumulation → Realization), 8-12 weeks
- **Sessions:** Full-body, A/B/C/D sessions with 6-block format (A-F)
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
2. Read `feature-tracker.json` for current project state and blockers.
3. Work within your file ownership scope.
4. End every session by updating `feature-tracker.json` with your changes.

## Session End Checklist
1. ✅ All prompt changes logged in `changelog.md`
2. ✅ Output schemas updated if prompt output structure changed
3. ✅ Tested against 3+ diverse personas
4. ✅ Coach responses stay in character and within boundaries
5. ✅ No medical claims or diagnoses in any prompt output
6. ✅ No real user data in any file
7. ✅ `feature-tracker.json` updated (status, blockers, schema changes)
