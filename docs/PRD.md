# PRODUCT REQUIREMENTS DOCUMENT
# Your Fitness Buddy

**AI-Powered Personalized Fitness Platform**

Version 2.1 (Combined) | February 2026 | Confidential

Quiz Funnel | AI Plan Generation | Workout Tracking | AI Coaching
Wearable Integration | Blood Panel Analytics | Supplement Marketplace | Nutrition Planning

---

1. EXECUTIVE SUMMARY

Your Fitness Buddy is an AI-powered fitness platform that delivers fully personalized, periodized training programs through a deep onboarding quiz, real-time workout tracking, an AI coaching system, wearable/body composition integration, blood panel analytics with automated supplement protocols, an integrated marketplace, and nutrition planning.

The platform targets 100+ fitness niches at scale by using a comprehensive 40+ question conditional quiz funnel that captures detailed user profiles, then generates custom periodized training plans using a proprietary methodology (Cressey-influenced, pull-dominant, periodized across strength/power/mobility phases). The AI coach — presented as a white-labeled, human-like persona — provides ongoing check-ins, adapts programs semi-adaptively based on logged performance, and answers user questions via open chat.

Business Model: Tiered SaaS (Free Basic + Pro + Business plans) with integrated marketplace revenue (supplements, beauty, telehealth), affiliate commissions, and anonymized market research data sales.
Platform: Web application first (responsive), native iOS and Android apps in a later phase.
Tech Stack: Supabase (database + auth + storage), Claude API (AI plan generation + coaching), Stripe (payments), React/Next.js (frontend).
Development Approach: Solo founder building with AI coding tools (Claude Code). No external dev team.

2. PRODUCT VISION & STRATEGY

2.1 Elevator Pitch
Your Fitness Buddy takes everything a world-class personal trainer knows — periodization, injury management, mobility, power development, nutrition, supplementation, and body composition tracking — and delivers it through an AI system that feels like a dedicated human coach, at a fraction of the cost, personalized to your exact body, goals, limitations, and lifestyle.

2.2 Competitive Differentiation

### What Makes YFB Different

1. **Real Periodization, Not Random Workouts:** Competitors (Fitbod, Caliber, Dr. Muscle, Juggernaut AI) generate individual workouts or use linear progression. YFB generates complete 12-week periodized macrocycles with phase-specific training qualities (foundation → accumulation → realization). The AI understands that Week 6 should feel fundamentally different from Week 2 — not just heavier.

2. **Methodology-First, Not Algorithm-First:** Most AI fitness apps use generic exercise databases and machine learning to suggest exercises. YFB encodes a specific, opinionated methodology (Cressey-influenced, pull-dominant, isometric-progressive) into the AI's system prompt. This means every plan follows the same principles a top-tier S&C coach would use — not what a recommendation engine thinks is popular.

3. **Full Session Architecture:** Competitors typically program main lifts and leave accessory work random. YFB generates complete sessions with 6 defined blocks (A through F), warm-up protocols, and session-specific exercise selection. Every training quality (strength, power, mobility, core, hypertrophy, tendon health) is programmed into every session.

4. **Injury-Aware Programming:** Not just "avoid this exercise." YFB builds prehab INTO the plan structure: Nordic curls for ACL history, scapular work for shoulder issues, pelvic floor-safe progressions for postpartum. The AI references injury-specific constraint rules, not generic flags.

5. **White-Label AI Coach:** The coach persona is NOT presented as AI. It's a named, consistent personality with domain expertise. No competitor offers this level of persona consistency.

6. **Niche Depth:** YFB targets 100+ fitness niches (postpartum, ACL rehab, martial arts, desk job athletes, etc.) with specific programming rules per niche. Competitors treat everyone like a general fitness client.

### Competitive Landscape

| Feature | YFB | Fitbod | Caliber | Juggernaut AI | TrainHeroic | Dr. Muscle |
|---------|-----|--------|---------|--------------|-------------|------------|
| Periodized macrocycle | 3-phase | Per-workout | Coach-dependent | Basic | Template-based | Per-set |
| Methodology-driven | Encoded | ML-based | Coach-dependent | Partial | Template | Algorithm |
| Full session blocks (A-F) | Yes | No | No | No | No | No |
| AI coaching persona | White-label | No | No | No | No | No |
| Injury-aware prehab | Built-in | Basic flags | Coach-dependent | No | No | Basic |
| Blood panel integration | Yes | No | No | No | No | No |
| Marketplace | Yes | No | No | No | No | No |

2.3 Target Market: 100+ Niches at Scale
Rather than targeting one customer avatar, the quiz funnel dynamically identifies and serves users across a matrix of dimensions:

A user who is a 42-year-old desk worker with a knee injury wanting fat loss with a home gym gets a completely different plan, messaging, and product experience than a 24-year-old martial artist wanting power and performance at a full gym.

3. USER PERSONAS & ROLES


3.1 The AI Coach (System Actor)
The AI Coach is not a user role but a system actor. It is white-labeled — presented to users as a human-like coaching persona with no explicit mention of AI. The AI Coach:
- Generates periodized training plans from quiz data using the founder's proprietary methodology
- Sends automated check-ins (weekly progress summaries, motivation, deload reminders)
- Responds to open-ended user questions about their program, injuries, form, and modifications
- Suggests plan adjustments semi-adaptively (user approves before changes are applied)
- Recommends supplements based on blood panel data and training phase
- Adjusts nutrition targets based on body composition trends
Personality: Warm, knowledgeable, direct, encouraging without being patronizing. Speaks like an experienced coach who genuinely cares about the client's progress. Uses the founder's training philosophy and voice.
System Prompt Foundation: The AI Coach's system prompt includes the complete training methodology (periodization structure, exercise selection principles, pull-to-push ratios, injury protocols, progression logic), the user's full quiz profile, their training history, and current program state.

4. FEATURE SPECIFICATION: QUIZ FUNNEL SYSTEM

4.1 Overview
Purpose: Capture comprehensive user profile data to generate a fully personalized training plan, segment users for marketing, and create a deeply resonant onboarding experience where users feel genuinely heard and understood.
Entry Points: 1) Standalone landing page (lead generation — email captured after results). 2) In-app for existing users (new plan generation or re-quiz every 12 weeks).
Length: 40+ questions across 30 conditional layers. Estimated completion time: 8-12 minutes.
Tone: Fun, realistic, deeply connecting. Every question should drive internal resonance — the user should be thinking 'yes... yes... yes... this is ME.' Not clinical. Not generic. Speaks directly to the customer's lived experience.

4.2 Conditional Logic Architecture
The quiz uses branching conditional logic across 30 layers. Each answer can trigger different follow-up questions. Example flow:

Q: 'Do you have any injuries or chronic pain?' → YES → Q: 'Which area?' → KNEE → Q: 'What type of knee issue?' → ACL/MCL/Meniscus/Patella/General → Q: 'Have you had surgery?' → YES → Q: 'How long ago?' → Q: 'Current pain level during exercise (1-10)?'

Q: 'Do you have any injuries or chronic pain?' → NO → Skip entire injury branch → Next category

This means a user with no injuries may answer 30 questions, while a user with multiple injuries, complex goals, and sport-specific needs may answer 50+.

4.3 Quiz Categories & Question Bank

4.3 Complete Quiz Question Bank (17 Categories, 40+ Core Questions)

CATEGORY 1: IDENTITY & DEMOGRAPHICS
• What should we call you? (first name — personalizes entire experience)
• How old are you? (age brackets with relatable copy: '36-45: The years where smart training beats hard training')
• What's your biological sex? (affects baseline recommendations, hormonal context)
• How tall are you? (critical for exercise selection — tall athletes need different movement patterns)
• What's your current weight? (baseline for body comp tracking)
• Where are you located? (timezone for check-ins, GDPR jurisdiction, language preference)

CATEGORY 2: GOALS & MOTIVATION
• What's the #1 thing you want from your training? (fat loss / muscle gain / athletic performance / longevity & health / rehab & pain-free movement / body recomp / sport-specific performance / general fitness)
• If you could change ONE thing about your body or fitness in the next 12 weeks, what would it be? (open text — rich data for personalization + marketing)
• How urgent does this feel? (casual / moderate / very important / this is my top priority right now)
• Have you tried to achieve this goal before? → YES → What happened? Why did it stop working? (open text — reveals objections and pain points for marketing)
• CONDITIONAL: If goal = sport-specific → Which sport? → How competitive? → What physical qualities does your sport demand most?
• CONDITIONAL: If goal = aesthetic → Which body areas are priority? → Physique reference points?

CATEGORY 3: TRAINING HISTORY & CURRENT STATUS
• How would you describe your training experience? (complete beginner / used to train but stopped / train inconsistently / train regularly 6+ months / train seriously 2+ years / competitive athlete)
• How many times per week do you currently exercise? (0 / 1-2 / 3-4 / 5+ )
• What does your current training look like? (no program / following YouTube/Instagram / app-based program / self-programmed / working with a coach) → reveals sophistication level
• CONDITIONAL: If training regularly → What's working? What's NOT working? (open text)
• CONDITIONAL: If has training history → Estimated max lifts or movement benchmarks? (squat, deadlift, bench, pull-up count, running pace — optional but valuable for calibrating starting loads)
• How long are your current sessions? (under 30 min / 30-45 / 45-60 / 60-75 / 75+ / don't currently train)

CATEGORY 4: EQUIPMENT & ENVIRONMENT
• Where do you train? (commercial gym / home gym / both / outdoors / hotel gyms when traveling / no equipment currently)
• CONDITIONAL: If home gym → What equipment do you have? (multi-select: barbell, dumbbells, kettlebells, pull-up bar, bench, squat rack, cables, bands, rings, cardio machine, foam roller, other)
• CONDITIONAL: If commercial gym → What type? (big box / boutique / CrossFit box / university / hotel / military)
• Is your training space ever a limitation? (space, noise, equipment availability, time slots)

CATEGORY 5: INJURIES, PAIN & LIMITATIONS
• Do you currently have any injuries or chronic pain that affects your training? → NO → skip
• CONDITIONAL: YES → Which areas? (multi-select: neck, shoulder, elbow/wrist, upper back, lower back, hip, knee, ankle/foot, other)
• CONDITIONAL: For EACH selected area → What type? (acute injury / chronic pain / post-surgery / stiffness/tightness / instability / nerve-related)
• CONDITIONAL: For EACH → Severity during exercise (1-10 scale)
• CONDITIONAL: For EACH → Have you had surgery? → When? → Current status?
• CONDITIONAL: For EACH → Specific movements that aggravate it?
• Are you currently working with a physiotherapist or doctor for any of these? (ensures we don't contradict medical advice)
• CONDITIONAL: Any movements you've been told to avoid?

CATEGORY 6: SPORT & ACTIVITY
• Do you play any sports or do structured physical activities outside the gym?
• CONDITIONAL: YES → Which? (multi-select with popular options + 'other')
• CONDITIONAL: For each → How many sessions per week?
• CONDITIONAL: For each → Competitive level? (recreational / club / competitive / professional)
• CONDITIONAL: For each → Which physical qualities matter most for your sport? (speed, power, endurance, agility, strength, flexibility, reaction time)
• How should your gym training support your sport? (improve performance / prevent injury / both / sport is casual — gym is primary focus)

CATEGORY 7: LIFESTYLE & DAILY LIFE
• What's your work situation? (desk job / active job / hybrid / remote / student / retired / stay-at-home parent / shift work)
• CONDITIONAL: If desk job → How many hours sitting per day? (triggers posture-specific programming)
• CONDITIONAL: If shift work → What shift pattern? (affects recovery and scheduling)
• How would you describe your daily stress level? (low / moderate / high / very high / it varies wildly)
• What recovery tools do you currently use? (multi-select: sauna, cold plunge, massage, foam rolling, stretching routine, meditation, yoga, none)
• How much time can you realistically dedicate to training per session? (30 min / 45 min / 60 min / 75 min / 90+ min)
• How many gym sessions per week can you commit to? (2 / 3 / 4 / 5 / 6 / flexible)
• Preferred training time? (early morning / morning / lunch / afternoon / evening / varies)

CATEGORY 8: SLEEP & RECOVERY
• How many hours of sleep do you typically get? (under 5 / 5-6 / 6-7 / 7-8 / 8+ )
• How would you rate your sleep quality? (terrible / poor / okay / good / excellent)
• Do you wake up during the night regularly? (no / sometimes / yes, multiple times)
• Do you use any sleep aids? (none / melatonin / magnesium / prescription / other)
• CONDITIONAL: If poor sleep → Do you think sleep affects your training recovery? (connects the dots for them — builds resonance)

CATEGORY 9: NUTRITION STATUS
• How would you describe your current diet? (no structure at all / trying to eat healthy but inconsistent / track calories loosely / track macros / follow a specific diet protocol / work with a nutritionist)
• Do you have any dietary restrictions? (multi-select: vegetarian, vegan, gluten-free, dairy-free, halal, kosher, keto, allergies, none)
• How many meals per day do you typically eat? (1-2 / 3 / 4-5 / 6+ / very irregular)
• Do you currently take any supplements? → YES → Which? (multi-select: protein powder, creatine, multivitamin, omega-3, vitamin D, magnesium, pre-workout, collagen, other)
• How important is nutrition optimization to you right now? (not a priority / somewhat important / very important / it's the missing piece)
• CONDITIONAL: If very important → Would you like meal plans and macro targets included in your program?

CATEGORY 10: MOVEMENT SCREENING (PROXY)
• Can you touch your toes with straight legs? (easily / just barely / not close — hamstring flexibility proxy)
• Can you hold a deep squat (thighs below parallel) for 30 seconds? (easily / with a struggle / can't get there — ankle/hip mobility proxy)
• Can you raise both arms straight overhead without arching your back? (easily / with some arch / restricted — shoulder/thoracic mobility proxy)
• Can you stand on one leg for 30 seconds with eyes closed? (easily / wobble a lot / can't do it — proprioception/balance proxy)
• Do you have any areas that feel consistently tight or restricted? (multi-select: hip flexors, hamstrings, ankles, shoulders, upper back, lower back, neck, none)

CATEGORY 11: PAIN MAPPING
• Beyond injuries, do you experience regular aches or discomfort? (yes / no)
• CONDITIONAL: YES → Where? (visual body map — tap to select areas)
• CONDITIONAL: For each → When does it occur? (during exercise / after exercise / when sitting / when waking up / all the time)
• CONDITIONAL: For each → Severity (1-10)
• CONDITIONAL: For each → Does it improve with movement/warm-up? (yes / no / sometimes — distinguishes structural vs. stiffness issues)

CATEGORY 12: TRAINING PERSONALITY & PREFERENCES
• Do you prefer variety in your workouts or consistent routines? (love variety / prefer routine / mix of both)
• Do you prefer training alone or with others? (alone / with a partner / group classes / don't care)
• Morning or evening trainer? (early bird / night owl / whenever I can fit it in)
• What motivates you most? (seeing numbers go up / looking better / feeling better / competition / health markers / social accountability)
• What has caused you to quit programs in the past? (multi-select: boredom, too complex, too time-consuming, no results, injury, life got busy, no accountability, program wasn't right for me)
• How do you feel about tracking data? (love it, give me all the metrics / I'll track the basics / just tell me what to do, I don't want to think about it)

CATEGORY 13: TECHNOLOGY & WEARABLES
• Do you currently use any fitness wearables or apps? (multi-select: Apple Watch, Garmin, Whoop, Oura, Fitbit, Renpho scale, MyFitnessPal, Cronometer, MacroFactor, none)
• Would you like your wearable data synced into your training program? (yes / not right now / I don't use wearables)
• Have you had blood work done in the last 12 months? (yes / no / not sure)
• CONDITIONAL: YES → Would you like to track your blood markers and get supplement recommendations based on them?

CATEGORY 14: BUDGET & COMMITMENT
• What do you currently spend monthly on fitness? (nothing / under $50 / $50-100 / $100-200 / $200+ — calibrates supplement and plan recommendations)
• How much would you invest monthly in a program that actually worked for you? (under $20 / $20-50 / $50-100 / $100+ / depends on results — pricing validation)
• Have you ever hired a personal trainer or online coach? → YES → What was the experience? → What was missing? (competitive intelligence)

CATEGORY 15: HORMONAL & METABOLIC INDICATORS
• Do you experience energy crashes during the day? (rarely / sometimes / frequently / daily)
• For male users: Have you noticed changes in energy, libido, or recovery in recent years? (no / somewhat / significantly — testosterone/hormonal flag)
• For female users: Are your menstrual cycles regular? Do you experience symptoms that affect training? (PMS, cramps, energy fluctuation — cycle-aware programming flag)
• CONDITIONAL: Age 40+ → Have you noticed changes in body composition despite consistent training/diet? (metabolic adaptation flag)
• Do you have any diagnosed hormonal or metabolic conditions? (thyroid, PCOS, diabetes, insulin resistance, none, prefer not to say)
• Are you currently on any medications that might affect training or body composition? (yes — specify / no / prefer not to say)

CATEGORY 16: AESTHETIC VS. PERFORMANCE
• On a scale: is your primary motivation more aesthetic (how you look) or performance (what you can do)? (slider: 100% aesthetic ←→ 100% performance)
• CONDITIONAL: If aesthetic-leaning → Which areas are priority? (multi-select body parts)
• CONDITIONAL: If performance-leaning → What specific performance goals? (open text: e.g., 'deadlift 2x bodyweight', 'run 5K under 25 min', 'compete in BJJ')
• Do you have a timeline for a specific event or goal? (vacation, competition, wedding, reunion, health milestone, no deadline)

CATEGORY 17: SOCIAL & ACCOUNTABILITY
• What level of accountability do you need? (self-motivated / occasional check-ins / regular check-ins / need someone watching over me)
• Have you successfully stuck with a program for 12+ weeks before? (yes / no / never tried one that long)
• What would make you most likely to stick with this program? (seeing results fast / enjoying the workouts / having a coach check in / tracking progress visually / social/community aspect)
• Is there anything else you want us to know about you, your body, your goals, or your life that would help us build the perfect program? (open text — often captures the most valuable insights)

4.4 Dynamic Results Page
After quiz completion, the user sees a personalized results page. This page is NOT AI-generated each time — it uses a template system populated from the database of answers.

Template Structure: The results page is built from modular content blocks that assemble dynamically based on the user's quiz profile:
1. HERO SECTION: Personalized headline addressing their #1 goal + primary limitation (e.g., 'Your 12-Week Plan for Building Power While Protecting Your Knee')
2. PROFILE SUMMARY: Visual summary of their inputs (height, weight, experience level, equipment, sport, injuries — displayed as tags/badges)
3. PLAN PREVIEW: Overview of their generated plan structure (phases, session types, weekly schedule) — enough to excite, not enough to replace paying
4. METHODOLOGY MATCH: Explains WHY this specific approach was chosen for THEM (e.g., 'Because you're 6'5" with a desk job, your plan prioritizes lunge-dominant lower body to protect your back...')
5. RISK CALLOUT: Addresses their specific injury/limitation with confidence (e.g., 'Your ACL history is factored into every exercise selection. Nordic curls are programmed every session for re-injury prevention.')
6. CTA: Email capture (if landing page entry) or upgrade prompt (if free user) or plan activation (if Pro/Business)

Niche Messaging: Each content block draws from a messaging library keyed to quiz dimensions. Example: a 'desk job' user sees copy about posture correction and hip flexor work. A 'martial artist' sees copy about rotational power and neck conditioning. A 'postpartum' user sees copy about core rebuilding and pelvic floor considerations. The copy library is managed in Supabase and editable by Admin.

4.5 Data Storage & Marketing Utilization
All quiz responses are stored in Supabase with the following structure:


Marketing Data Utilization
1. EMAIL SEGMENTATION: Auto-tag users into segments (e.g., 'beginners with knee injuries', 'advanced martial artists', 'desk workers wanting fat loss'). Trigger targeted email sequences per segment.
2. AD TARGETING: Export segment data for Facebook/Meta lookalike audiences. Build custom audiences from quiz dimensions (e.g., all users aged 35-45 with home gyms wanting muscle gain).
3. CONTENT STRATEGY: Dashboard showing which goals, injuries, sports, and pain points are most common — directly informs blog, video, and ad creative production.
4. ANONYMIZED MARKET RESEARCH: Aggregate, anonymize, and package quiz data for sale to fitness industry brands (supplement companies, equipment manufacturers, gym chains). Requires separate consent flow under GDPR.

5. FEATURE SPECIFICATION: AI PLAN GENERATION ENGINE

5.1 Overview
The AI Plan Generation Engine takes the complete user profile from the quiz and generates a fully periodized, multi-phase training program. The AI uses the founder's proprietary methodology as its foundational framework — not generic fitness best practices.

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
• Exercise selection: Drawn from a curated exercise bank (linked to Eric Cressey resources + founder's preferred movements)

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

This ensures 2x/week frequency for each accessory pair while keeping individual sessions to 2 F Block exercises (not 4). Programming all 4 accessories in every session adds 8 unnecessary sets and was identified as a critical programming error during methodology validation.

### 5.2.3 E Block Session Specificity (v3.1)

E Block exercises MUST vary by session to target different muscle groups:
- Session A: Biceps, Lateral Raise, Quad accessory
- Session B: Triceps, Rear Delt, Traps
- Session C: Rows (high rep), Glutes, Lats
- Session D: Combo movements, Band Pull-Aparts

### 5.2.4 Mandatory Session Inclusions (v3.1)

Regardless of user profile, every generated plan MUST include:
1. Nordic curl variant in B1 position of every session (ACL prehab)
2. Neck strengthening in D4 position of every session (martial arts/sport safety)
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
The plan is NOT static once generated. The AI monitors logged performance and suggests adjustments:


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
• OFFLINE MODE: Session data cached locally, syncs to Supabase when connection restores (critical for gym basements with poor signal).

7. FEATURE SPECIFICATION: AI COACH SYSTEM

7.1 Automated Check-ins

7.2 Open Conversational Chat
Users can message the AI coach at any time with questions. The AI has access to:
• Complete user quiz profile
• Current program state (phase, week, session)
• Full training log history
• Body composition trends (if wearable connected)
• Blood panel data (if entered)
• Supplement protocol status
• The founder's complete methodology framework

Boundaries: The AI coach does NOT diagnose medical conditions, prescribe medication, override physiotherapist/doctor advice, or make claims about curing diseases. When health questions exceed its scope, it recommends professional consultation. Standard medical disclaimers are displayed.

7.3 White-Label Presentation
The AI coach presents as a named persona (name TBD by founder). No mention of AI, Claude, or algorithms in any user-facing copy. The persona has a consistent voice: warm, knowledgeable, direct, encouraging without being patronizing. Responses are formatted as natural coaching messages, not AI-style bullet points.

8. FEATURE SPECIFICATION: WEARABLE & BODY COMPOSITION INTEGRATION

8.1 Integration Priority

8.2 Body Composition Dashboard
• Historical trend charts: weight, body fat %, muscle mass, visceral fat — plotted over full program duration
• Phase overlay: vertical markers showing Phase 1/2/3 transitions on trend charts
• Goal progress: visual indicator of progress toward body comp goals set in quiz
• AI insight: When body comp data shows a trend (gaining muscle while losing fat, plateau, unexpected gain), AI coach comments on it proactively

9. FEATURE SPECIFICATION: BLOOD PANEL & SUPPLEMENT PROTOCOL

9.1 Blood Panel Entry
Users manually enter blood test results. The system tracks the following markers over time:


9.2 Automated Supplement Protocol
Based on blood markers, training phase, quiz profile, and body composition data, the system generates and maintains a supplement protocol:

• DEFICIENCY CORRECTION: If Vitamin D < 30 ng/mL → recommend Vitamin D3 + K2 at specific dosage, link to marketplace product
• PERFORMANCE OPTIMIZATION: If in Phase 2 (max strength) and creatine not in current stack → recommend creatine monohydrate
• RECOVERY SUPPORT: If inflammation markers elevated + high training load → recommend omega-3, magnesium, curcumin
• HORMONAL SUPPORT: If testosterone trending low + male 35+ → recommend zinc, vitamin D, ashwagandha, lifestyle modifications
• SLEEP SUPPORT: If sleep quality poor (from readiness scores) → recommend magnesium glycinate, recommended sleep hygiene practices

Protocol updates: Re-evaluated when new blood panel data is entered, when training phase changes, or when body composition data shows significant shifts.
Disclaimers: All supplement recommendations include medical disclaimers. Users are advised to consult their physician. The system does not diagnose, treat, or prescribe. Supplement recommendations are educational, not medical advice.

10. FEATURE SPECIFICATION: MARKETPLACE

10.1 Overview
An integrated marketplace within the app for supplements, beauty products, and telehealth services. Revenue model: own-brand products + affiliate commissions + marketplace fees.

10.2 Product Categories

10.3 Marketplace-Plan Integration
The marketplace is not a standalone store — it's contextually integrated into the training experience:
• AI coach recommends supplements → direct link to marketplace product
• Blood panel shows deficiency → supplement card appears with 'Add to Cart'
• Exercise requires equipment user doesn't have → equipment recommendation with purchase link
• Skincare/beauty products recommended based on hormonal and lifestyle profile from quiz

10.4 Technical: Stripe Integration
• Stripe for all payment processing (subscriptions + marketplace purchases)
• Cart/checkout flow within the app (no redirect to external site)
• Subscription management (upgrade/downgrade/cancel) via Stripe Customer Portal
• Marketplace orders: Stripe checkout → order stored in Supabase → fulfillment trigger (own brand) or affiliate redirect (partner products)

11. FEATURE SPECIFICATION: NUTRITION & MEAL PLANNING

11.1 Philosophy
The nutrition system follows a longevity-focused, whole-foods approach: high protein, satiating, nutrient-dense, minimally processed. Not a restrictive 'diet' — a sustainable way of eating for performance and health.

11.2 Meal Plan Generator
AI generates weekly meal plans based on:
• Macro targets (calculated from body comp goals, weight, activity level, training phase)
• Dietary restrictions (from quiz: vegetarian, vegan, allergies, etc.)
• Food preferences (from quiz or learned over time from food log)
• Budget considerations (from quiz)
• Meal frequency preference (from quiz)
• Training day vs. rest day calorie cycling (higher carbs on training days)

11.3 Food Logging & Macro Tracker
• Search food database (integrate open food facts or similar)
• Barcode scanner (post-MVP, mobile only)
• Quick-add meals from generated meal plans
• Daily macro dashboard: protein / carbs / fat / calories vs. targets
• Weekly adherence trends
• Integration with Cronometer/MacroFactor for users who prefer those tools


12. TECHNICAL ARCHITECTURE (UPDATED FOR MULTI-AGENT)
12.1 Stack Overview
The technology stack remains the same as v1.0: Supabase (database, auth, storage, edge functions), Claude API (AI plan generation, coaching, analysis), Stripe (payments), React/Next.js (frontend), deployed on Vercel. The key change in v2.1 is how these components are organized across repositories, how Claude Code agents interact with them, and the guardrail infrastructure that keeps agents in scope.

See `docs/ARCHITECTURE.md` in each repo for WHY each architectural decision was made (multi-repo rationale, Vercel choice, Supabase choice, Claude API model selection, PWA/offline strategy).
12.2 Three-Repository Architecture
The project is split into three independent Git repositories, each owned by a specific set of Claude Code agents. This separation enforces clean boundaries and enables parallel development without merge conflicts.

12.3 Architecture Data Flow
The system data flow across repositories follows this pattern:

User interacts with yfb-frontend (quiz, session logger, coach chat, dashboard).
Frontend calls Supabase client SDK for auth, data reads, and realtime subscriptions.
For AI-powered features, frontend triggers Supabase Edge Functions in yfb-backend.
Edge Functions load system prompts from yfb-ai-prompts (bundled at deploy time or fetched from shared storage).
Edge Functions call Claude API with assembled prompts + user data, parse structured JSON responses, and store results in Supabase.
Frontend receives results via Supabase realtime or polling.

Critical rule: The frontend NEVER calls the Claude API directly. All AI interactions are mediated through Edge Functions to protect API keys and enforce rate limits.


12A. MULTI-AGENT ORCHESTRATION ARCHITECTURE
12A.1 Why Multi-Agent
A project of this complexity exceeds what a single Claude Code session can hold in context. The multi-agent approach solves this by giving each agent a focused scope, its own CLAUDE.md instruction file, and strict file ownership boundaries. This prevents context overflow, naming drift, and cross-cutting bugs.

v2.1 adds concrete guardrail infrastructure to enforce these boundaries:
- `feature-tracker.json` in each repo: Token-efficient status tracker (~200 tokens vs 2,000+ prose). Agents read at session start for current project state, update at session end.
- `.claude/hooks.json` in each repo: Exit Code 2 hooks block cross-repo file edits, TypeScript `any` type usage, and `.env` access at the tool level — before code even reaches CI.
- `.claude/settings.json` in each repo: MCP CLI mode configuration saves context window budget by connecting to Supabase, GitHub, and Vercel directly.
- `.github/workflows/ci.yml` in frontend + backend repos: Automated lint, type-check, build, and test on every PR.
- `tsconfig.json` with all strict mode flags: NON-NEGOTIABLE for AI-assisted development — catches type errors that agents create.
12A.2 Agent Roles
Six specialized agent roles operate across the three repositories. Each role is activated at the start of a Claude Code session with a role declaration prompt. Agents MUST NOT modify files outside their ownership scope.

12A.3 Session Orchestration Strategy
For MVP development (Phases 1–2), all sessions run SEQUENTIALLY. One agent completes its work, commits, and the next agent picks up with a fresh context that references the previous session's output. This eliminates merge conflicts and coordination overhead.

Parallel sessions are only introduced in Phase 3+ when the architecture is stable and agents work on completely independent features in separate repos with no shared files.

Sequential session flow for a typical feature:
Backend Agent: Create database tables + RLS policies + Edge Function skeleton. Commit with API contract in message.
AI Agent: Write system prompts + output schema + test with 3+ personas. Commit.
Backend Agent: Wire Edge Function to load prompts, call Claude API, parse response, store result. Commit.
Frontend Agent: Build UI consuming the API contract documented in Backend commits. Commit.
Full-Stack Agent (if needed): Integration testing across all layers. Fix contract mismatches. Commit.
12A.4 CLAUDE.md Files
Each repository contains a CLAUDE.md file that Claude Code reads at session start. This is the most important file in each repo. It defines: project overview, tech stack, coding rules, file ownership scope, what the agent can and cannot modify, naming conventions, and integration points with other repos.

The CLAUDE.md files are the source of truth for agent behavior. They reference `feature-tracker.json` for current project state and `docs/ARCHITECTURE.md` for architectural rationale. They are maintained by the DevOps Agent and updated when architectural decisions change. Full specifications are provided in the Technical Implementation Guide v2.1.


12B. AGENT COMMUNICATION PROTOCOL
12B.1 Contract-First Development
Agents communicate through interface contracts, not direct coordination. When the Backend Agent creates an API endpoint, the contract (URL, method, request body schema, response schema, error codes) is documented in the git commit message. The Frontend Agent then builds against this contract without needing to understand the backend implementation.

This mirrors how real engineering teams work: the API contract is the agreement between teams. If a contract changes, the changing agent documents the breaking change and the consuming agent updates accordingly.
12B.2 Shared Type System
TypeScript interfaces that cross repo boundaries (e.g., QuizProfile, TrainingPlan, SessionLog) are defined in a shared types location. The yfb-frontend/src/types/ directory is the canonical source. The backend Edge Functions maintain equivalent Zod schemas for runtime validation. The AI Agent's output-schema.json files must match these types exactly.

When a type changes, the change propagates: types/ updated first, then Zod schemas, then output schemas. This is enforced through the session handoff protocol.
12B.3 Handoff Protocol
Every Claude Code session ends with a structured handoff that enables the next session to pick up without context loss:

Update feature-tracker.json: Mark features as complete, update blockers, add new contracts.
Session Summary: What was built, files modified, tests added.
Interface Contracts: API endpoints created, component props, database schema changes.
Known Issues: Bugs, workarounds, technical debt.
Next Session Tasks: Prioritized list with recommended agent role.
Dependencies/Blockers: What's waiting on other work.

Session summaries are stored in a SESSION_LOGS.md file in each repository root and referenced when starting new sessions. The feature-tracker.json provides a token-efficient snapshot of the entire project state without reading prose logs.
12B.4 Prompt Versioning and Backend Sync
AI prompts in yfb-ai-prompts are versioned independently. When a prompt changes, the AI Agent updates changelog.md with the date, what changed, and test results. The Backend Agent then updates the Edge Function to reference the new prompt version. Prompts are bundled into Edge Functions at deploy time (not fetched at runtime) to ensure consistency and avoid latency.


12C. REPOSITORY OWNERSHIP MAP
12C.1 yfb-frontend Ownership
Frontend Agent OWNS:
src/app/ (all pages and routes)
src/components/ (all UI components)
src/hooks/ (custom React hooks)
src/stores/ (Zustand state management)
src/styles/ (theme tokens, design system)
src/types/ (TypeScript type definitions — canonical source for shared types)
public/locales/ (i18n translation files)
tests/ (Playwright E2E and component tests)

Frontend Agent READS but does NOT modify:
src/lib/supabase/ (Supabase client config — maintained by Backend Agent)
src/lib/stripe/ (Stripe client helpers — maintained by Integration Agent)
12C.2 yfb-backend Ownership
Backend Agent OWNS:
supabase/migrations/ (all SQL migration files)
supabase/functions/ (all Edge Functions)
scripts/ (seed scripts, data export)
data/ (exercise bank, quiz questions, niche messaging JSON)

Integration Agent OWNS (within yfb-backend):
Edge Functions for third-party services (stripe-webhook, stripe-checkout, renpho-sync)
Third-party API client code
12C.3 yfb-ai-prompts Ownership
AI Agent OWNS:
prompts/ (all system prompts, methodology docs, personality definitions)
tests/personas/ (synthetic test profiles)
Output schema JSON files
changelog.md

This repo contains NO application code. It is purely prompts, documentation, schemas, and test data.
12C.4 Cross-Repo Dependencies




13. DATA MODEL & DATABASE SCHEMA (SUPABASE)

13.1 Core Tables

14. PHASED ROADMAP & TIMELINE

Given solo development with AI coding tools, realistic timeline estimates account for learning curves, debugging, and iteration. Each phase includes buffer time.


Total estimated timeline to full product: 7-10 months from start of development, assuming full-time effort with AI coding tools.
MVP launch: 8-12 weeks. This is the fastest path to revenue and user validation.

15. MONETIZATION & PRICING


15.1 Revenue Streams
1. SUBSCRIPTIONS: Pro and Business tier monthly/annual recurring revenue
2. MARKETPLACE: Own-brand product margins (40-60%), affiliate commissions (15-30%), telehealth referral fees
3. DATA: Anonymized, aggregated quiz and user data sold to fitness industry brands (requires separate GDPR consent)
4. FUTURE: White-label licensing (other coaches/brands use the platform under their own branding)

16. MARKETING & DATA STRATEGY

16.1 Quiz as Marketing Engine
The quiz funnel is the primary acquisition channel. It serves dual purposes: product onboarding AND lead generation.

Landing Page Flow: Ad (Facebook/Instagram/TikTok) → Landing page with quiz CTA → Quiz (no account required) → Results page (email capture gate) → Account creation → Plan preview (Free) → Upgrade CTA (Pro/Business)

Ad Strategy (100+ Niches): Each niche combination generates a unique ad angle. Example ads:
• 'Desk job destroying your posture? Take the 5-minute assessment and get a plan built for your body.' (targets: desk workers)
• 'Training around a knee injury shouldn't mean giving up your goals.' (targets: injury recovery)
• 'Most martial artists train like bodybuilders. Here's what you should be doing instead.' (targets: martial artists)
• 'Over 40 and losing muscle despite eating well? Your hormones might be the missing piece.' (targets: 40+ hormonal)

16.2 Data Utilization Pipeline
Quiz Data → Supabase → Segmentation Engine → Three outputs:
1. EMAIL SEQUENCES: Automated nurture sequences per segment (beginners get educational content, advanced users get performance tips, injury users get rehab content)
2. AD AUDIENCES: Weekly export of segment data for Meta/Google lookalike audience building
3. B2B REPORTS: Quarterly anonymized market research reports (e.g., '68% of home gym users aged 30-45 report knee pain as their #1 training limitation' — valuable to equipment companies, supplement brands, physiotherapy chains)

17. LEGAL, COMPLIANCE & GDPR

17.1 GDPR Compliance (Mandatory — DACH/Nordic Markets)
Health and fitness data is classified as 'special category data' under GDPR Article 9. This requires:


17.2 Health Claims & Disclaimers
• The app does NOT diagnose, treat, cure, or prevent any disease.
• Supplement recommendations are educational, not medical prescriptions.
• Blood panel interpretation is informational — users must consult a healthcare provider for medical decisions.
• AI coach is a fitness guidance tool, not a licensed healthcare professional.
• All health-related screens include visible disclaimers.
• Terms of service include liability limitation for health outcomes.

17.3 EU Market Regulatory Considerations
• EU MEDICAL DEVICE REGULATION (MDR): If the app's blood panel analysis or supplement recommendations are deemed 'clinical decision support', it may classify as a medical device under EU MDR. RISK MITIGATION: Frame all recommendations as 'educational wellness guidance', not clinical recommendations. Include clear disclaimers. Consult a regulatory attorney before launch.
• FTC (if US market): Supplement marketing must not make unsubstantiated health claims. Testimonials require disclaimers.
• SUPPLEMENT LABELING: If selling own-brand supplements, must comply with EU Food Supplement Directive (2002/46/EC) and local market regulations.
• WHITE-LABELING AI: Not disclosing AI use raises ethical considerations. While not currently illegal, transparency trends may require disclosure in the future. RECOMMENDATION: Use language like 'AI-assisted coaching' in Terms of Service even if not prominent in UI.

17.4 Stripe & App Store Compliance
• Apple App Store requires in-app purchases for digital goods/subscriptions (30% commission). Physical goods (supplements) can use external payment.
• Stripe handles PCI compliance for payment data. No credit card data stored in Supabase.
• Subscription cancellation must be easy and accessible (consumer protection regulations).

18. EXERCISE VIDEO PRODUCTION PIPELINE

18.1 Overview
Exercise demonstration videos are AI-generated using tools like Sora, Kling, or Veo3. This is an ADMIN/PRODUCTION feature, not user-facing. Users see finished videos; they do not interact with the generation pipeline.

18.2 Production Workflow
1. EXERCISE BANK AUDIT: Identify all unique exercises across all possible plan variations (~150-200 exercises)
2. PROMPT ENGINEERING: Create standardized prompts per exercise (camera angle, lighting, athlete appearance, movement speed, key form cues to highlight)
3. BATCH GENERATION: Generate videos in batches using selected AI video tool
4. QA REVIEW: Admin reviews each video for form accuracy, visual quality, and appropriateness
5. UPLOAD & LINK: Approved videos uploaded to Supabase Storage and linked to exercise_bank records
6. ONGOING: New exercises added to bank trigger video production pipeline

Admin UI Feature: A 'Video Production' section in the admin dashboard showing: exercises without videos, video generation queue, QA review queue, and published videos. This is a productivity tool for the founder, not a customer feature.

19. DESIGN SYSTEM & BRAND IDENTITY

Brand identity needs to be built from scratch. The design system must feel premium, trustworthy, and energetic — not generic 'fitness app.'

19.1 Brand Identity Requirements

### Visual Identity

**Color Palette:**
- Primary: Deep Navy (#1B2A4A) — trust, authority, premium feel
- Accent: Electric Teal (#00C9A7) — energy, health, modern
- Warm: Coral (#FF6B6B) — motivation, intensity markers
- Background: Off-white (#F8F9FA) — clean, breathable
- Dark mode: Charcoal (#1E1E2E) with same accent colors

**Typography:**
- Headings: Inter (bold weight) — clean, modern, tech-forward
- Body: Inter (regular) — excellent readability
- Data/Numbers: JetBrains Mono — workout stats, timers, rep counters

**UI Personality:**
- Clean, not clinical. Athletic, not aggressive. Premium, not minimalist-for-the-sake-of-it.
- Reference apps for inspiration: Whoop (data presentation), Peloton (motivation/community feel), Calm (premium simplicity), Notion (information density done right)
- Dark mode is the default for gym use (OLED-friendly, low eye strain under fluorescent lights)
- Animations: subtle, purposeful. Progress rings fill on log completion. Session blocks slide in sequentially.

**AI Coach Visual Persona:**
- No robot avatars, no generic fitness stock photos
- The coach persona has a custom illustrated avatar (commissioned post-MVP)
- Chat interface looks like iMessage, not a help desk

19.2 Dark Mode Specification
Default: Dark mode. User can toggle to light mode. Preference persisted in local storage + Supabase user settings.


19.3 Component Library
Build a reusable component library from day 1 using Tailwind CSS + shadcn/ui as the foundation. Core components:

• Buttons: primary, secondary, ghost, destructive. All with loading states, disabled states.
• Cards: exercise card, session card, metric card, marketplace product card. Consistent padding/radius.
• Forms: text input, number input, select, multi-select, slider (for RPE, pain scale), toggle, radio, checkbox.
• Data display: stat card (big number + label + trend arrow), chart wrapper, progress bar, streak indicator.
• Navigation: bottom tab bar (mobile), sidebar (desktop), breadcrumbs, back button.
• Feedback: toast notifications, modal dialogs, confirmation sheets, loading skeletons.
• Timer: circular countdown, rest timer overlay, session clock.
• Chat: message bubble (coach vs. user), typing indicator, message input with send button.

19.4 Data Visualization (Whoop-Style)
Charts and data displays follow a data-rich but organized approach, inspired by Whoop's dashboard:

• PRIMARY METRICS: Large hero cards with current value, trend direction, and sparkline. (e.g., Body Weight: 92.4kg ↓ 0.3kg this week [sparkline])
• TREND CHARTS: Line charts with phase overlays (vertical markers at Phase 1/2/3 transitions). Time range selector (1W, 1M, 3M, ALL).
• PROGRESS RINGS: Circular progress indicators for weekly targets (sessions completed, macro adherence, readiness average).
• HEATMAPS: Weekly training heatmap showing session intensity by day (like GitHub contribution graph).
• COMPARISON: Side-by-side current vs. previous cycle metrics. Before/after body comp comparisons.
• LIBRARY: Use Recharts (React) for charts. Consistent color coding across all visualizations.

20. UX PATTERNS & INTERACTION DESIGN

20.1 First-Session Onboarding
Approach: Guided walkthrough using contextual tooltips on the first session. Not a separate tutorial — the user learns by doing.

Step 1: After quiz + plan generation, user lands on dashboard. Tooltip: 'Here’s your training plan. Today is Session A. Tap to start.'
Step 2: On session screen, tooltip highlights readiness assessment: 'Quick check-in before you train. Rate how you’re feeling today.'
Step 3: First exercise appears. Tooltip: 'Here’s your first exercise. The target is on the left. Log your actual performance on the right.'
Step 4: After first set logged, tooltip: 'Rest timer started. When it’s done, log your next set.'
Step 5: Session complete. Tooltip: 'Session logged. Your coach will check in later with feedback.'
After first session: tooltips don’t repeat unless user resets onboarding in settings.

20.2 Notification Strategy
Philosophy: Adaptive frequency. More frequent during first 2 weeks to build habits, then taper to avoid fatigue. User controls final frequency in settings.


20.3 AI Coach Chat Rate Limits

Abuse prevention: AI coach system prompt scoped strictly to fitness, nutrition, health, and the user’s program. Off-topic queries receive a friendly redirect: 'I’m here to help with your training and health. What can I help you with regarding your program?' Token limit per message: 500 tokens output. Long-form analysis (weekly summaries) generated server-side on schedule, not via chat.

20.4 Offline Behavior (PWA)
• SESSION TRACKING: Full offline support. Current session’s exercises, prescriptions, and logging UI are cached in the service worker. User can complete entire session offline.
• DATA SYNC: When connection restores, all logged data (sets, reps, loads, RPE, readiness, session notes) syncs to Supabase with conflict resolution (last-write-wins, timestamped).
• AI COACH: Not available offline. Chat shows: 'You’re offline. Your coach will respond when you’re back online.'
• DASHBOARD: Last-fetched data displayed with 'Last updated: [timestamp]' indicator.
• PLAN VIEW: Full plan (all phases, all sessions) cached locally after first load. No server call needed to view upcoming workouts.

20.5 Plan Versioning
When the founder updates the methodology or exercise bank, existing users are notified via AI coach message:

'We’ve updated our training methodology with new exercises and improved programming. You have two options: 1) Continue your current plan as-is and get the updates when your next cycle starts. 2) Regenerate your plan now with the latest methodology (your quiz profile and training history are preserved). What would you prefer?'

• Option 1: Plan remains unchanged until 12-week cycle completes. Next plan generation uses updated methodology.
• Option 2: AI regenerates plan mid-cycle. New plan starts from current week number (not week 1). Training history informs starting loads.
• Previous plan versions are archived in Supabase (never deleted). User can view past plans.

21. ACCESSIBILITY (WCAG 2.1 AA)

WCAG 2.1 AA compliance is legally required for EU markets (European Accessibility Act, effective June 2025). This is not optional.


21.1 Gym-Specific Accessibility
• LARGE TOUCH TARGETS: Minimum 48x48px tap targets (WCAG) but prefer 56x56px for sweaty gym hands on phone screens.
• HIGH CONTRAST MODE: Beyond standard dark/light, offer a high-contrast toggle for outdoor/bright-gym use.
• AUDIO + HAPTIC: Rest timer uses audio beep + phone vibration + visual countdown. Never relies on only one modality.
• TEXT SCALING: Respect system font size preferences. UI must remain functional at 200% text zoom.
• ONE-HAND OPERATION: Session logging UI designed for one-hand thumb-zone operation (critical when holding a dumbbell in the other hand).
• VOICE INPUT: Explore voice-to-log capability (post-MVP): 'Log 30 kilos, 8 reps' between sets without touching phone.

22. INTERNATIONALIZATION (i18n)

Launch Languages: English (primary), German (DACH), Swedish, Danish, Norwegian.
Framework: next-intl with JSON locale files. All user-facing strings extracted to locale files from day 1 — no hardcoded strings.


22.1 Translation Workflow
1. All new features developed in English first
2. Strings extracted to en.json locale file
3. AI-assisted translation (Claude) for draft translations
4. Professional review for DE (priority market), community review for SV/DA/NO
5. Exercise names: always professionally translated
6. Legal documents: always professionally translated by a legal translator

23. SOFTWARE ENGINEERING STANDARDS

23.1 Error Handling & Resilience

### Claude API Failures

**Scenario:** Claude API returns 500 or times out after 30s during plan generation.
**User sees:** Full-screen message: "Your coach is putting the finishing touches on your plan. This is taking a bit longer than usual. We'll keep trying."
**System behavior:** Exponential backoff retry (5s, 15s, 30s, 60s). After 4 failed attempts, show: "We couldn't generate your plan right now. Your quiz answers are saved — we'll have your plan ready within the next hour. We'll send a push notification when it's done."
**Backend:** Queue the generation request in a retry table. Background worker retries every 15 minutes for 4 hours. If still failing, alert the ops team.

**Scenario:** Claude API fails during coach chat.
**User sees:** "Your coach stepped away for a moment. Your message is saved — they'll respond shortly." with retry button.
**System behavior:** 3 retries with 5s backoff. After failure, queue message for async response.

### Stripe Failures

**Scenario:** Stripe checkout fails mid-payment.
**User sees:** "We couldn't process your payment. Your cart is saved. Please try again or use a different payment method." No cart data is lost.
**System behavior:** Log error to PostHog. Never show raw Stripe error messages to user. Retry on user's next attempt.

**Scenario:** Subscription renewal fails.
**User sees:** Email + in-app banner: "Your subscription payment failed. Update your payment method to keep your plan active." 3-day grace period before downgrade.

### Supabase Outage

**Scenario:** Supabase is unreachable during workout logging.
**User sees:** Nothing changes — session continues offline.
**System behavior:** All workout data cached in local storage (IndexedDB). Sync queue builds. When connection restores, sync all cached data with conflict resolution (local wins if newer). This is critical — gym basements have poor signal.

### Graceful Degradation Priority

1. Workout logging MUST work offline (highest priority — never lose a user's training data)
2. Coach chat degrades to queued messages (async is acceptable)
3. Plan generation degrades to queued generation (async is acceptable)
4. Marketplace degrades to "temporarily unavailable" message

23.2 Security
• AUTHENTICATION: Supabase Auth with email/password + social (Google, Apple). Email verification required. Password requirements: 8+ chars, 1 uppercase, 1 number.
• ROW LEVEL SECURITY (RLS): Supabase RLS policies on every table. Users can only read/write their own data. Admin role has elevated access via custom claims.
• API KEYS: All API keys (Claude, Stripe, Renpho) stored as environment variables. Never exposed to client-side code. All AI calls routed through server-side edge functions.
• RATE LIMITING: API endpoints rate-limited per user (e.g., plan generation: 1 per 12 hours, chat: 20 messages/day for Pro).
• DATA ENCRYPTION: Supabase encrypts data at rest (AES-256). All traffic over HTTPS/TLS 1.3. Blood panel and health data treated as sensitive — additional column-level encryption considered.
• INPUT SANITIZATION: All user inputs sanitized server-side. Quiz open-text fields validated and escaped before storage and before injection into AI prompts (prevent prompt injection).
• CSRF/XSS: Next.js built-in CSRF protection. Content Security Policy headers. No dangerouslySetInnerHTML.

23.3 Performance Targets

### Web Vitals Budgets

| Metric | Target | Measurement |
|--------|--------|-------------|
| LCP (Largest Contentful Paint) | < 2.5s | 75th percentile, mobile 4G |
| FID (First Input Delay) | < 100ms | 75th percentile |
| CLS (Cumulative Layout Shift) | < 0.1 | 75th percentile |
| TTFB (Time to First Byte) | < 800ms | Vercel Edge Network |

### Feature-Specific Targets

| Feature | Target | Notes |
|---------|--------|-------|
| Quiz page load | < 1.5s | Pre-rendered, no API calls until interaction |
| Plan generation | < 45s | User sees progress animation during generation |
| Coach chat response | < 5s | Sonnet model, streaming response displayed as typing |
| Session logger load | < 2s | Today's session pre-fetched on app open |
| Workout log save | < 1s | Optimistic UI — show saved immediately, sync async |
| Exercise swap | < 2s | Substitution list pre-cached |
| Dashboard load | < 3s | Charts rendered client-side from cached data |

### Bundle Size Budgets

| Route | JS Budget | Notes |
|-------|-----------|-------|
| Landing page | < 100KB | Static, no heavy dependencies |
| Quiz | < 150KB | Multi-step form, conditional logic |
| Session logger | < 200KB | Timer, logging UI, exercise data |
| Dashboard | < 250KB | Charting library (Recharts) |

### CI Enforcement

All performance budgets are enforced in the GitHub Actions CI pipeline. PRs that exceed budgets are blocked with a descriptive error. The DevOps Agent configures Lighthouse CI in `.github/workflows/ci.yml`.

23.4 Testing Strategy
• AI PLAN VALIDATION: Build a test suite of 20+ persona profiles covering edge cases (multiple injuries + minimal equipment + beginner, advanced athlete + sport-specific + desk job, etc.). Generate plans for each. Human review for safety and quality. Automated checks for: no contraindicated exercises for flagged injuries, correct phase structure, pull-to-push ratio enforcement, deload week presence.
• QUIZ LOGIC: Automated tests for every conditional branch. Verify correct questions appear for every answer combination. Track completion rate and drop-off by question.
• E2E TESTS: Playwright for critical user flows: quiz completion, plan generation, session logging, payment, account creation/deletion.
• ACCESSIBILITY AUDITS: axe-core automated scans in CI pipeline. Manual screen reader testing quarterly. Contrast ratio checks on every new component.
• LOAD TESTING: Verify Supabase and Claude API can handle projected concurrent users (start with 100 concurrent, scale testing as user base grows).

23.5 Database Backups & Disaster Recovery
• Supabase Pro plan includes daily automated backups with point-in-time recovery (up to 7 days).
• AI-generated plans are expensive to regenerate — plans are NEVER deleted, only archived. Stored as structured JSON in training_plans table.
• Weekly manual backup export of critical tables (users, quiz_profiles, training_plans, session_logs) to separate cloud storage (e.g., Cloudflare R2 or AWS S3).
• Disaster recovery target: RPO (Recovery Point Objective) < 24 hours. RTO (Recovery Time Objective) < 4 hours.

23.6 Monitoring & Observability
• ERROR TRACKING: Sentry for frontend + edge function error tracking. Alert on error rate spikes.
• ANALYTICS: PostHog for product analytics (quiz funnel conversion, feature usage, retention cohorts, session frequency).
• AI COSTS: Custom dashboard tracking Claude API spend per user, per feature (plan gen vs. chat vs. supplement analysis). Alert if cost/user exceeds threshold.
• UPTIME: Vercel + Supabase built-in monitoring. External uptime monitor (BetterUptime or similar) for public-facing pages.

24. OPEN QUESTIONS & RISKS
