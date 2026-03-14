# PRODUCT REQUIREMENTS DOCUMENT
# Your Fitness Buddy

**Personal AI-Powered Fitness Tool**

Version 3.0 | March 2026

Quiz Onboarding | AI Plan Generation | Workout Tracking | AI Coaching
Wearable Integration | Blood Panel Analytics

---

1. EXECUTIVE SUMMARY

Your Fitness Buddy is a personal fitness tool for Jarnail. It delivers a fully personalized, periodized training program through a deep onboarding quiz, real-time workout tracking, an AI coaching system, wearable/body composition integration, and blood panel analytics with supplement protocols.

The quiz captures a detailed profile, then generates custom periodized training plans using a proprietary Cressey-influenced methodology. The AI coach provides ongoing check-ins, adapts programs semi-adaptively based on logged performance, and answers questions via open chat.

Tech Stack: Supabase (database + auth + storage), Claude API (AI plan generation + coaching), React/Next.js (frontend, self-hosted or Supabase serving).
Development: Solo build using Claude Code as the primary development tool.

---

2. PRODUCT VISION

2.1 Elevator Pitch
Your Fitness Buddy takes everything a world-class personal trainer knows — periodization, injury management, mobility, power development, supplementation, and body composition tracking — and delivers it through an AI system that feels like a dedicated human coach, personalized to Jarnail's exact body, goals, limitations, and lifestyle.

2.2 What Makes This Different (Methodology First)

1. **Real Periodization, Not Random Workouts:** Generates complete 12-week periodized macrocycles with phase-specific training qualities (foundation → accumulation → realization). Week 6 feels fundamentally different from Week 2 — not just heavier.

2. **Methodology-First, Not Algorithm-First:** A specific, opinionated methodology (Cressey-influenced, pull-dominant, isometric-progressive) is encoded into the AI's system prompt. Every plan follows the same principles a top-tier S&C coach would use.

3. **Full Session Architecture:** Generates complete sessions with 6 defined blocks (A through F), warm-up protocols, and session-specific exercise selection. Every training quality (strength, power, mobility, core, hypertrophy, tendon health) is programmed into every session.

4. **Injury-Aware Programming:** Builds prehab INTO the plan structure. Nordic curls for ACL history, scapular work for shoulder issues. References injury-specific constraint rules, not generic flags.

5. **Consistent AI Coach Persona:** The coach has a named personality with domain expertise and consistent voice.

---

3. USER ROLES

3.1 Jarnail (Primary User)
The sole user of this tool. Uses it to follow his periodized training plan, log workouts, check in with the AI coach, and track body composition and blood markers over time.

3.2 The AI Coach (System Actor)
Not a user role but a system actor. Presented as a named coaching persona. The AI Coach:
- Generates periodized training plans from quiz data using the proprietary methodology
- Sends automated check-ins (weekly progress summaries, deload reminders)
- Responds to open-ended questions about the program, injuries, form, and modifications
- Suggests plan adjustments semi-adaptively (user approves before changes are applied)
- Recommends supplements based on blood panel data and training phase
System Prompt Foundation: Includes the complete training methodology, full quiz profile, training history, and current program state.

---

4. FEATURE SPECIFICATION: QUIZ FUNNEL SYSTEM

4.1 Overview
Purpose: Capture a comprehensive profile to generate a fully personalized training plan. Used at onboarding and re-run every 12 weeks to generate the next plan.
Length: 40+ questions across 30 conditional layers. Estimated completion time: 8-12 minutes.
Tone: Specific and direct. Every question helps produce a more accurate plan.

4.2 Conditional Logic Architecture
The quiz uses branching conditional logic across 30 layers. Each answer can trigger different follow-up questions. Example flow:

Q: 'Do you have any injuries or chronic pain?' → YES → Q: 'Which area?' → KNEE → Q: 'What type of knee issue?' → Q: 'Have you had surgery?' → Q: 'How long ago?' → Q: 'Current pain level during exercise (1-10)?'

Q: 'Do you have any injuries or chronic pain?' → NO → Skip entire injury branch → Next category

A user with no injuries may answer 30 questions. A user with multiple injuries and sport-specific needs may answer 50+.

4.3 Quiz Categories & Question Bank

CATEGORY 1: IDENTITY & DEMOGRAPHICS
• What should we call you? (first name — personalizes experience)
• How old are you?
• What's your biological sex?
• How tall are you?
• What's your current weight?
• Where are you located? (timezone for check-ins)

CATEGORY 2: GOALS & MOTIVATION
• What's the #1 thing you want from your training? (fat loss / muscle gain / athletic performance / longevity / rehab & pain-free movement / body recomp / sport-specific performance / general fitness)
• If you could change ONE thing about your body or fitness in the next 12 weeks, what would it be? (open text)
• How urgent does this feel?
• Have you tried to achieve this goal before? → YES → What happened? Why did it stop working?
• CONDITIONAL: If goal = sport-specific → Which sport? → How competitive? → What physical qualities does your sport demand most?

CATEGORY 3: TRAINING HISTORY & CURRENT STATUS
• How would you describe your training experience? (complete beginner / used to train but stopped / train inconsistently / train regularly 6+ months / train seriously 2+ years / competitive athlete)
• How many times per week do you currently exercise?
• What does your current training look like?
• CONDITIONAL: If training regularly → What's working? What's NOT working?
• CONDITIONAL: If has training history → Estimated max lifts or movement benchmarks?
• How long are your current sessions?

CATEGORY 4: EQUIPMENT & ENVIRONMENT
• Where do you train? (commercial gym / home gym / both / outdoors / no equipment)
• CONDITIONAL: If home gym → What equipment do you have?
• CONDITIONAL: If commercial gym → What type?
• Is your training space ever a limitation?

CATEGORY 5: INJURIES, PAIN & LIMITATIONS
• Do you currently have any injuries or chronic pain that affects your training? → NO → skip
• CONDITIONAL: YES → Which areas?
• CONDITIONAL: For EACH selected area → What type? (acute / chronic / post-surgery / stiffness / instability / nerve-related)
• CONDITIONAL: For EACH → Severity during exercise (1-10)
• CONDITIONAL: For EACH → Have you had surgery? → When? → Current status?
• CONDITIONAL: For EACH → Specific movements that aggravate it?
• Are you currently working with a physiotherapist or doctor for any of these?
• CONDITIONAL: Any movements you've been told to avoid?

CATEGORY 6: SPORT & ACTIVITY
• Do you play any sports or do structured physical activities outside the gym?
• CONDITIONAL: YES → Which? How many sessions/week? Competitive level? Which physical qualities matter most?
• How should your gym training support your sport?

CATEGORY 7: LIFESTYLE & DAILY LIFE
• What's your work situation? (desk job / active job / hybrid / remote / student / retired / shift work)
• CONDITIONAL: If desk job → How many hours sitting per day?
• How would you describe your daily stress level?
• What recovery tools do you currently use?
• How much time can you realistically dedicate to training per session?
• How many gym sessions per week can you commit to?

CATEGORY 8: SLEEP & RECOVERY
• How many hours of sleep do you typically get?
• How would you rate your sleep quality?
• Do you wake up during the night regularly?
• Do you use any sleep aids?

CATEGORY 9: NUTRITION STATUS
• How would you describe your current diet?
• Do you have any dietary restrictions?
• How many meals per day do you typically eat?
• Do you currently take any supplements?
• How important is nutrition optimization to you right now?

CATEGORY 10: MOVEMENT SCREENING (PROXY)
• Can you touch your toes with straight legs?
• Can you hold a deep squat (thighs below parallel) for 30 seconds?
• Can you raise both arms straight overhead without arching your back?
• Can you stand on one leg for 30 seconds with eyes closed?
• Do you have any areas that feel consistently tight or restricted?

CATEGORY 11: PAIN MAPPING
• Beyond injuries, do you experience regular aches or discomfort?
• CONDITIONAL: YES → Where? When does it occur? Severity? Does it improve with movement/warm-up?

CATEGORY 12: TRAINING PERSONALITY & PREFERENCES
• Do you prefer variety in your workouts or consistent routines?
• What motivates you most?
• What has caused you to quit programs in the past?
• How do you feel about tracking data?

CATEGORY 13: TECHNOLOGY & WEARABLES
• Do you currently use any fitness wearables or apps?
• Would you like your wearable data synced into your training program?
• Have you had blood work done in the last 12 months?
• CONDITIONAL: YES → Would you like to track your blood markers and get supplement recommendations?

CATEGORY 14: HORMONAL & METABOLIC INDICATORS
• Do you experience energy crashes during the day?
• For male users: Have you noticed changes in energy, libido, or recovery in recent years?
• CONDITIONAL: Age 40+ → Have you noticed changes in body composition despite consistent training/diet?
• Do you have any diagnosed hormonal or metabolic conditions?
• Are you currently on any medications that might affect training or body composition?

CATEGORY 15: AESTHETIC VS. PERFORMANCE
• Is your primary motivation more aesthetic (how you look) or performance (what you can do)?
• CONDITIONAL: If aesthetic-leaning → Which areas are priority?
• CONDITIONAL: If performance-leaning → What specific performance goals?
• Do you have a timeline for a specific event or goal?

CATEGORY 16: SOCIAL & ACCOUNTABILITY
• What level of accountability do you need?
• Have you successfully stuck with a program for 12+ weeks before?
• Is there anything else you want us to know?

4.4 Results Page
After quiz completion, the user sees a personalized results summary. Structure:
1. HERO SECTION: Personalized headline addressing their #1 goal + primary limitation
2. PROFILE SUMMARY: Visual summary of their inputs (height, weight, experience, equipment, sport, injuries — tags/badges)
3. PLAN PREVIEW: Overview of plan structure (phases, session types, weekly schedule)
4. METHODOLOGY MATCH: Explains WHY this approach was chosen (e.g., 'Because of your desk job, your plan prioritizes lunge-dominant lower body to protect your back...')
5. RISK CALLOUT: Addresses specific injury/limitation with confidence
6. PLAN ACTIVATION: Direct access to the generated plan

---

5. FEATURE SPECIFICATION: AI PLAN GENERATION ENGINE

5.1 Overview
The AI Plan Generation Engine takes the complete user profile from the quiz and generates a fully periodized, multi-phase training program using the proprietary methodology as its foundational framework.

5.2 Methodology Framework (Baked into AI)
The following training principles are encoded into the AI's system prompt and plan generation logic:
• Periodization: 3-phase macrocycle (Foundation → Accumulation → Realization) across 8-12 weeks
• Session structure: Full-body sessions with A/B/C/D block format (Primary Strength → Secondary + Rotation → Isometric + End-Range → Core Circuit)
• Session rotation: A (sagittal dominant), B (frontal/rotational), C (posterior chain) — all three performed weekly
• Pull-to-push ratio: 3:2 minimum across all sessions
• Lower body: Lunge/split-squat dominant for joint health (no heavy back squats as default)
• Warm-up: Cressey-influenced movement preparation (foam rolling → movement prep → neural activation)
• Isometrics: Yielding → Overcoming → Functional → Reactive progression across phases
• End-range training: PAILs/RAILs → loaded stretches → dynamic end-range across phases
• Core: Anti-movement patterns → loaded rotational → explosive/reactive across phases
• Nordic curls: Eccentric-only → full range → reactive across phases (ACL/hamstring prehab)
• Deload: Every 4th week (40-50% volume reduction)
• Exercise selection: Drawn from a curated exercise bank

### 5.2.1 Block Taxonomy (v3.1)

Every standard session (A, B, C) contains 6 execution blocks in fixed order:

- **A Block — Primary Strength** (15-18 min): Main compound lift + antagonist superset. Phase determines rep range: P1 3×8-10, P2 4×4-6, P3 3×3-4 + explosive contrast.
- **B Block — Secondary + Rotation** (12-15 min): 3 exercises. Nordic curl in B1 (mandatory — ACL prehab), pressing in B2, rotation in B3.
- **C Block — Isometric + End-Range** (10-12 min): 3-4 exercises. Progression: yielding (P1) → overcoming (P2) → reactive (P3). Pistol squat progression tracked here.
- **D Block — Core Circuit** (8-10 min): 3-4 exercises. Anti-movement (P1) → loaded (P2) → explosive (P3). Neck work in D4 every session.
- **E Block — Hypertrophy** (8-10 min): 2-3 exercises. Session-specific selection (NOT identical across sessions). Joint protection and aesthetic work.
- **F Block — Accessory** (8-10 min): 2 exercises per session. DISTRIBUTED across the week: calf/tibialis on lower days (A,C), dead hang/wrist roller on upper days (B,D). Never all 4 accessories in one session.

Session D uses a unique phase-specific structure (not the standard A-F template). See `block-taxonomy.md`.

### 5.2.2 Accessory Distribution Rule (v3.1)

The AI plan generation engine MUST distribute F Block exercises strategically:
- Sessions A & C (lower emphasis): SL Calf Raise + Tibialis Raise
- Sessions B & D (upper emphasis): Dead Hang + Wrist Roller

### 5.2.3 E Block Session Specificity (v3.1)

E Block exercises MUST vary by session to target different muscle groups:
- Session A: Biceps, Lateral Raise, Quad accessory
- Session B: Triceps, Rear Delt, Traps
- Session C: Rows (high rep), Glutes, Lats
- Session D: Combo movements, Band Pull-Aparts

### 5.2.4 Mandatory Session Inclusions (v3.1)

Regardless of user profile, every generated plan MUST include:
1. Nordic curl variant in B1 position of every session (ACL prehab)
2. Neck strengthening in D4 position of every session (sport safety)
3. CARs (hips + shoulders) in every warm-up
4. Band pull-aparts in every warm-up
5. Pull-to-push ratio ≥ 3:2 verified per session

5.3 Plan Generation Flow
1. Quiz completion triggers plan generation
2. System constructs an AI prompt containing: full user profile, methodology framework, exercise bank, constraints (equipment, injuries, time, frequency)
3. Claude API generates the complete plan (all phases, all sessions, all weeks, all exercises with sets/reps/tempo/load/RPE/progression notes)
4. Plan is parsed and stored in Supabase as structured data (not raw text)
5. User sees plan in the app as interactive sessions they can navigate and log against
6. AI validates generated plan against `plan-generation-constraints.md` (15-point checklist)
7. Plan is structured as JSON per `plan-generation-output-schema.json` with validation_checks object confirming all constraints pass
8. If any validation check fails, the AI corrects the plan and re-validates before storing

### 5.3.1 Constraint Files (v3.1)

The plan generation system prompt references these files from `yfb-ai-prompts/prompts/plan-generation/`:

| File | Purpose |
|------|---------|
| `plan-generation-constraints.md` | 15-point validation checklist (hard rules) |
| `output-schema.json` | Exact JSON structure for Supabase storage |
| `progression-rules.json` | Per-block, per-phase progression rules |
| `block-taxonomy.md` | Complete block structure reference |
| `exercise-bank-schema.json` | Exercise database with categories, equipment, substitutions |

5.4 Semi-Adaptive Adjustment System
The plan is NOT static once generated. The AI monitors logged performance and suggests adjustments based on: RPE trends, completion rates, injury flags, and body composition shifts. User approves all adjustments before they're applied.

---

6. FEATURE SPECIFICATION: WORKOUT TRACKING & SESSION LOGGER

6.1 Session Flow (User Experience)
1. User opens app → sees today's scheduled session (e.g., 'Session B — Phase 2, Week 6')
2. Taps 'Start Session' → Readiness assessment (5 quick sliders: sleep, energy, motivation, soreness, joint stiffness) → Score auto-calculated → Intensity adjustment suggested if needed
3. Warm-up protocol displayed (checkable list — user taps through each exercise)
4. First exercise block appears: exercise name, target sets/reps/tempo/RPE, coaching cue, and video demo
5. User logs each set: load (kg/lbs), reps completed, RPE (optional per set). Rest timer auto-starts after each set.
6. After all sets → next exercise. Superset pairs displayed together with alternating indicators.
7. Session complete → summary screen: total volume, session RPE, time, notes field, comparison to last time this session was performed

6.2 Features
• REST TIMER: Configurable per block (default: A=120s, B=90s, C=45s, D=20s). Audio + haptic alert. Visual countdown. Overridable.
• SET LOGGING: Per-set load + reps + RPE. Auto-fills previous session's values as starting point. Swipe to add/remove sets.
• EXERCISE SWAP: Tap exercise → see substitution options from exercise bank → swap in-session without losing tracking data.
• SUPERSET INDICATOR: Visual pairing of A1/A2, B1/B2 etc. with 'next exercise' prompts.
• TEMPO GUIDE: Visual metronome/animation showing eccentric-pause-concentric-pause timing.
• HISTORY COMPARISON: During each exercise, show last session's performance (load/reps/RPE) for easy progressive overload decisions.
• SESSION NOTES: Free text field at end of session for subjective notes.
• OFFLINE MODE: Session data cached locally, syncs to Supabase when connection restores.

---

7. FEATURE SPECIFICATION: AI COACH SYSTEM

7.1 Automated Check-ins
The AI coach sends proactive messages:
• Weekly progress summaries (every Sunday)
• Deload week reminders (every 4th week)
• Phase transition messages when entering a new phase
• Adjustment suggestions when performance trends indicate change

7.2 Open Conversational Chat
Users can message the AI coach at any time with questions. The AI has access to:
• Complete user quiz profile
• Current program state (phase, week, session)
• Full training log history
• Body composition trends (if wearable connected)
• Blood panel data (if entered)
• Supplement protocol status
• The complete methodology framework

Boundaries: The AI coach does NOT diagnose medical conditions, prescribe medication, override physiotherapist/doctor advice, or make claims about curing diseases. When health questions exceed its scope, it recommends professional consultation.

7.3 Coach Persona
The AI coach presents as a named persona with a consistent voice: warm, knowledgeable, direct, encouraging without being patronizing. Responses are formatted as natural coaching messages. The persona is consistent across all interactions — check-ins, chat, and plan notes use the same voice.

---

8. FEATURE SPECIFICATION: WEARABLE & BODY COMPOSITION INTEGRATION

8.1 Integration Priority
Primary: Renpho smart scale (body composition — weight, body fat %, muscle mass, visceral fat)
Secondary: Apple Watch / Garmin (HRV, sleep, active calories — for readiness context)

8.2 Body Composition Dashboard
• Historical trend charts: weight, body fat %, muscle mass, visceral fat — plotted over full program duration
• Phase overlay: vertical markers showing Phase 1/2/3 transitions on trend charts
• Goal progress: visual indicator of progress toward body comp goals set in quiz
• AI insight: When body comp data shows a trend (gaining muscle while losing fat, plateau, unexpected gain), AI coach comments on it proactively

---

9. FEATURE SPECIFICATION: BLOOD PANEL & SUPPLEMENT PROTOCOL

9.1 Blood Panel Entry
Users manually enter blood test results. The system tracks the following markers over time:
• Hormonal: Testosterone (total + free), Estradiol, SHBG, DHEA-S, Cortisol
• Metabolic: Fasting glucose, HbA1c, Insulin, Thyroid (TSH, T3, T4)
• Cardiovascular: Total cholesterol, LDL, HDL, Triglycerides, CRP, Homocysteine
• Nutritional: Vitamin D, B12, Ferritin, Magnesium, Zinc, Iron
• Performance: IGF-1, ALT, AST, Creatinine, eGFR

9.2 Automated Supplement Protocol
Based on blood markers, training phase, quiz profile, and body composition data, the system generates and maintains a supplement protocol:

• DEFICIENCY CORRECTION: If Vitamin D < 30 ng/mL → recommend Vitamin D3 + K2 at specific dosage
• PERFORMANCE OPTIMIZATION: If in Phase 2 (max strength) and creatine not in current stack → recommend creatine monohydrate
• RECOVERY SUPPORT: If inflammation markers elevated + high training load → recommend omega-3, magnesium, curcumin
• HORMONAL SUPPORT: If testosterone trending low + male 35+ → recommend zinc, vitamin D, ashwagandha, lifestyle modifications
• SLEEP SUPPORT: If sleep quality poor (from readiness scores) → recommend magnesium glycinate, sleep hygiene practices

Protocol updates: Re-evaluated when new blood panel data is entered, when training phase changes, or when body composition data shows significant shifts.
Disclaimers: All supplement recommendations include medical disclaimers. Recommendations are educational, not medical advice.

---

12. TECHNICAL ARCHITECTURE

12.1 Stack Overview
- **Frontend:** Next.js 14+ (App Router, PWA), TypeScript strict, Tailwind + shadcn/ui, Supabase JS client, Recharts
- **Backend:** Supabase (PostgreSQL, Edge Functions, Auth, Storage, Realtime)
- **AI:** Anthropic Claude API (Opus for plan generation, Sonnet for coach chat)
- **Deployment:** Self-hosted or Supabase hosting (no Vercel dependency)

12.2 Single-Repo Mental Model
One developer, one codebase mental model across three repos (frontend, backend, ai-prompts). No multi-agent coordination overhead. Read the relevant CLAUDE.md and build.

12.3 Data Flow

```
User Browser
    │
    ▼
[Next.js App]  ──── Server Components (SSR) ────►  Supabase Client (reads, RLS-scoped)
    │
    │ (user actions)
    ▼
[Supabase Edge Functions]
    │
    ├── generate-plan/     → Claude Opus API  → parse output-schema.json → store plan
    ├── coach-chat/        → Claude Sonnet API → stream response
    ├── renpho-sync/       → Renpho API → store body comp data
    └── analyze-blood-panel/ → Claude Sonnet API → supplement recommendations
```

Key principle: Frontend NEVER calls Claude directly. All AI requests go through Edge Functions.

---

13. DATA MODEL & DATABASE SCHEMA (SUPABASE)

See `yfb-backend/supabase/migrations/` for canonical schema. Key tables:
- `profiles` — User profile and preferences
- `quiz_responses` — Quiz answers (jsonb)
- `training_plans` — Generated plans (plan_data jsonb + normalized tables)
- `plan_phases`, `plan_sessions`, `plan_session_exercises` — Normalized plan structure
- `session_logs` — Logged workouts with readiness assessment
- `set_logs` — Per-set data (load, reps, RPE)
- `quiz_categories`, `quiz_questions`, `exercise_bank` — Reference data

---

14. ROADMAP

Personal build timeline — no revenue milestones.

**Sprint 1 (complete):** Foundation — Next.js setup, Supabase schema, auth, quiz data seeded, quiz-resume Edge Function, exercise bank (95 exercises)

**Sprint 2 (complete):** AI Plan Generation — generate-plan Edge Function, coach-chat, coach-checkin Edge Functions

**Sprint 3:** Frontend plan viewer — display generated plan, phase/session navigation

**Sprint 4:** Session tracker — core gym UI, set logging, rest timer, offline mode

**Sprint 5:** Dashboard + body comp — Whoop-style data display, Renpho integration

**Sprint 6:** Blood panel + supplement protocol UI

**Sprint 7:** Polish — notifications, plan versioning, settings

---

17. HEALTH CLAIMS & DISCLAIMERS

• The app does NOT diagnose, treat, cure, or prevent any disease.
• Supplement recommendations are educational, not medical prescriptions.
• Blood panel interpretation is informational — consult a healthcare provider for medical decisions.
• AI coach is a fitness guidance tool, not a licensed healthcare professional.
• All health-related screens include visible disclaimers.

---

19. DESIGN SYSTEM & BRAND IDENTITY

19.1 Visual Identity

**Color Palette:**
- Primary: Deep Navy (#1B2A4A) — trust, authority, premium feel
- Accent: Electric Teal (#00C9A7) — energy, health, modern
- Warm: Coral (#FF6B6B) — motivation, intensity markers
- Background: Off-white (#F8F9FA) — clean, breathable
- Dark mode: Charcoal (#1E1E2E) with same accent colors

**Typography:**
- Headings: Inter (bold weight)
- Body: Inter (regular)
- Data/Numbers: JetBrains Mono — workout stats, timers, rep counters

**UI Personality:**
- Clean, not clinical. Athletic, not aggressive. Premium, not minimalist-for-the-sake-of-it.
- Reference apps: Whoop (data presentation), Calm (premium simplicity), Notion (information density)
- Dark mode is the default for gym use (OLED-friendly)
- Animations: subtle, purposeful. Progress rings fill on log completion.

**AI Coach Visual Persona:**
- No robot avatars. Chat interface looks like iMessage, not a help desk.

19.2 Dark Mode Specification
Default: Dark mode. Light mode toggle. Preference persisted in local storage + Supabase user settings.

19.3 Component Library
Core components built on Tailwind CSS + shadcn/ui:
• Buttons: primary, secondary, ghost, destructive. All with loading states, disabled states.
• Cards: exercise card, session card, metric card. Consistent padding/radius.
• Forms: text input, number input, select, multi-select, slider (RPE, pain scale), toggle, radio, checkbox.
• Data display: stat card (big number + label + trend arrow), chart wrapper, progress bar, streak indicator.
• Navigation: bottom tab bar (mobile), sidebar (desktop), breadcrumbs.
• Feedback: toast notifications, modal dialogs, confirmation sheets, loading skeletons.
• Timer: circular countdown, rest timer overlay, session clock.
• Chat: message bubble (coach vs. user), typing indicator, message input with send button.

19.4 Data Visualization (Whoop-Style)
• PRIMARY METRICS: Large hero cards with current value, trend direction, and sparkline.
• TREND CHARTS: Line charts with phase overlays. Time range selector (1W, 1M, 3M, ALL).
• PROGRESS RINGS: Circular progress indicators for weekly targets.
• HEATMAPS: Weekly training heatmap showing session intensity by day.
• LIBRARY: Recharts for all charts. Consistent color coding.

---

20. UX PATTERNS & INTERACTION DESIGN

20.1 First-Session Onboarding
Guided walkthrough using contextual tooltips on the first session. Not a separate tutorial — user learns by doing.

Step 1: After quiz + plan generation, user lands on dashboard. Tooltip: 'Here's your training plan. Today is Session A. Tap to start.'
Step 2: On session screen, tooltip highlights readiness assessment.
Step 3: First exercise appears. Tooltip: 'Here's your first exercise. Log your actual performance on the right.'
Step 4: After first set logged, tooltip: 'Rest timer started.'
Step 5: Session complete. Tooltip: 'Session logged. Your coach will check in later with feedback.'

20.2 Notification Strategy
Philosophy: Adaptive frequency. More frequent during first 2 weeks to build habits, then taper. User controls frequency in settings.
Types: Scheduled session reminders, weekly check-in from AI coach, deload week notification, streak preservation alert.

20.3 AI Coach Chat
Scoped strictly to fitness, nutrition, health, and the user's program. Token limit per message: 500 tokens output. Long-form analysis (weekly summaries) generated server-side on schedule, not via chat.

20.4 Offline Behavior (PWA)
• SESSION TRACKING: Full offline support. Current session's exercises, prescriptions, and logging UI cached in service worker.
• DATA SYNC: When connection restores, all logged data syncs to Supabase (last-write-wins, timestamped).
• AI COACH: Not available offline. Chat shows offline indicator.
• PLAN VIEW: Full plan cached locally after first load.

20.5 Plan Versioning
When methodology or exercise bank updates, user is notified via AI coach message with option to continue current plan or regenerate with latest methodology (preserving quiz profile and training history). Previous plan versions are archived (never deleted).

---

21. ACCESSIBILITY (WCAG 2.1 AA)

21.1 Gym-Specific Accessibility
• LARGE TOUCH TARGETS: Minimum 48x48px tap targets. Prefer 56x56px for gym use.
• HIGH CONTRAST MODE: High-contrast toggle for bright-gym use.
• AUDIO + HAPTIC: Rest timer uses audio beep + vibration + visual countdown.
• TEXT SCALING: Respect system font size preferences. Functional at 200% text zoom.
• ONE-HAND OPERATION: Session logging UI designed for one-hand thumb-zone operation.

---

23. SOFTWARE ENGINEERING STANDARDS

23.1 Error Handling & Resilience

**Claude API Failures:**
Plan generation: Exponential backoff retry (5s, 15s, 30s, 60s). After 4 failed attempts, queue the generation request for retry. Notify user when ready.
Coach chat: 3 retries with 5s backoff. After failure, queue message for async response.

**Supabase Outage:**
Workout logging continues offline. All data cached in IndexedDB. Sync queue builds. When connection restores, sync all cached data with conflict resolution (local wins if newer). Critical — never lose a user's training data.

**Graceful Degradation Priority:**
1. Workout logging MUST work offline (highest priority)
2. Coach chat degrades to queued messages (async is acceptable)
3. Plan generation degrades to queued generation (async is acceptable)

23.2 Security
• AUTHENTICATION: Supabase Auth with email/password + social (Google, Apple). Email verification required.
• ROW LEVEL SECURITY (RLS): Supabase RLS policies on every table. Users can only read/write their own data.
• API KEYS: All API keys (Claude, Renpho) stored as environment variables. Never exposed to client-side code.
• INPUT SANITIZATION: All user inputs sanitized server-side. Quiz open-text fields validated and escaped before storage and before injection into AI prompts (prevent prompt injection).
• CSRF/XSS: Next.js built-in CSRF protection. Content Security Policy headers.

23.3 Performance Targets

| Feature | Target |
|---------|--------|
| Plan generation | < 45s |
| Coach chat response | < 5s (streaming) |
| Session logger load | < 2s |
| Workout log save | < 1s (optimistic UI) |
| Dashboard load | < 3s |

23.4 Testing Strategy
• AI PLAN VALIDATION: Test suite of 8+ persona profiles covering edge cases. Generate plans for each. Automated checks for: no contraindicated exercises, correct phase structure, pull-to-push ratio, deload week presence.
• QUIZ LOGIC: Automated tests for every conditional branch.
• ACCESSIBILITY AUDITS: axe-core automated scans. Contrast ratio checks on every new component.

23.5 Database Backups & Disaster Recovery
• Supabase Pro plan includes daily automated backups with point-in-time recovery.
• AI-generated plans are NEVER deleted, only archived.
• Disaster recovery target: RPO < 24 hours. RTO < 4 hours.

23.6 Monitoring & Observability
• ERROR TRACKING: Sentry for frontend + edge function error tracking.
• AI COSTS: Track Claude API spend per feature (plan gen vs. chat vs. supplement analysis). Alert if cost exceeds threshold.
• UPTIME: Supabase built-in monitoring.
