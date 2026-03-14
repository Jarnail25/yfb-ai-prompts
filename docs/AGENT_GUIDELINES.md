# Development Guidelines — Your Fitness Buddy

Solo development conventions for yfb-ai-prompts. For architecture decisions, see ARCHITECTURE.md. For tech stack and sprint plan, see TECH_GUIDE.md.

---

## Core Rules

1. ALL prompts in Markdown (`.md`). Never embed prompts in code.
2. Use `{{variable}}` for dynamic injection (`{{user_name}}`, `{{quiz_profile}}`).
3. EVERY change documented in `changelog.md` with date + reason.
4. Output schemas (JSON) define EXACT structure. Edge Functions parse against these.
5. Test personas must cover edge cases: injuries + minimal equipment, advanced athletes, seniors.
6. `prompts/plan-generation/methodology.md` is **GROUND TRUTH**. Plan gen prompts reference it, never contradict.
7. `prompts/coach-chat/personality.md` is **GROUND TRUTH** for coach voice. All coach comms must be consistent.
8. NEVER include real user data in any file. Synthetic test data only.
9. DO NOT modify application code. This repo is prompts, docs, schemas, and test data ONLY.
10. When changing output schemas, update `changelog.md` and ensure the backend Edge Function is aware of the change.

---

## Prompt Authoring Conventions

- Write prompts as if briefing a highly skilled contractor who has no prior context. Be explicit.
- Use numbered lists for sequential steps. Use bullet lists for non-ordered options.
- Constraint statements use MUST / MUST NOT / NEVER. Guidance uses "prefer" or "aim for".
- Every prompt references the relevant schema file for output structure.
- Variable injections (`{{variable}}`) go at the END of the system prompt, not mid-document.

---

## Output Schema Versioning

Schemas are versioned in `changelog.md`. When a breaking change is made:
1. Update the schema file.
2. Log the change in `changelog.md` with the version bump and what changed.
3. Note in the changelog that the backend generate-plan Edge Function must be updated to match.

Current schema: `output-schema.json` v3.1 — 6-block A-F structure, validation_checks, warm_ups, deload_protocol, readiness_assessment.

Backend note: The existing generate-plan Edge Function must be updated to handle 6 blocks (E: Hypertrophy, F: Accessory) and the new top-level fields.

---

## Test Persona Coverage

Maintain at least 8 personas that together cover:
- Beginner with injury + limited equipment
- Advanced athlete with full gym
- Senior with multiple limitations
- Desk worker (posture/hip issues)
- Return-to-training (deconditioning)
- Sport-specific (martial arts or team sport)
- 40+ hormonal considerations
- No injuries, commercial gym, general fitness goal

---

## Session Checklist

Before ending any session on this repo:
1. All prompt changes logged in `changelog.md`
2. Output schemas updated if prompt output structure changed
3. Tested against 3+ diverse personas before finalizing a new prompt
4. Coach responses stay in character and within boundaries
5. No medical claims or diagnoses in any prompt output
6. No real user data in any file
7. `feature-tracker.json` updated (status, blockers, schema changes)
