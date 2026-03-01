# PLAN GENERATION CONSTRAINTS
## Hard Rules for AI Plan Generation Engine

Version 1.0 | March 2026 | Repository: yfb-ai-prompts/prompts/plan-generation/

---

## Purpose

These are NON-NEGOTIABLE constraints the AI plan generation engine must enforce when generating any training plan. The system prompt must include these rules verbatim. Violation of any hard constraint means the plan is invalid and must be regenerated.

---

## STRUCTURAL CONSTRAINTS

### SC-1: Session Block Order
Every standard session (A, B, C) MUST contain blocks in this exact order: A → B → C → D → E → F. No block may be skipped or reordered.

### SC-2: Session D Unique Architecture
Session D uses a phase-specific structure that differs from Sessions A-C. The plan generation engine must select the correct Session D template based on the current phase. Session D does NOT use the same A-F block pattern.

### SC-3: Exercise Count Per Block
| Block | Min Exercises | Max Exercises |
|-------|--------------|--------------|
| A | 2 | 4 (Phase 3 contrast pairs) |
| B | 3 | 3 |
| C | 3 | 4 |
| D | 3 | 4 |
| E | 2 | 3 |
| F | 2 | 2 |

### SC-4: Total Exercises Per Session
Standard sessions (A-C): 16-20 exercises total (including warm-up as separate protocol, not counted in blocks).
Session D: 12-16 exercises total (lighter volume day).

### SC-5: Session Duration Targets
| Session Type | Phase 1 | Phase 2 | Phase 3 |
|-------------|---------|---------|---------|
| A, B, C | 70-80 min | 75-85 min | 70-80 min |
| D (optional) | 55-65 min | 60-70 min | 55-65 min |
| Warm-up | 12-15 min | 12-15 min | 12-15 min |

---

## PERIODIZATION CONSTRAINTS

### PC-1: Phase Structure (Non-negotiable)
- Phase 1 (Foundation): Weeks 1-4
- Phase 2 (Accumulation): Weeks 5-8
- Phase 3 (Realization): Weeks 9-12
- No deviation allowed regardless of user preference. The macrocycle IS the methodology.

### PC-2: Deload Weeks (Non-negotiable)
- Week 4: Deload (40-50% volume reduction)
- Week 8: Deload (40-50% volume reduction)
- Week 12: Test week / deload
- Implementation: Drop 1-2 sets per exercise, reduce load to 60-70% of peak week, cap RPE at 5-6

### PC-3: Rep Ranges Per Phase
| Phase | A Block | B Block | C Block | D Block | E Block |
|-------|---------|---------|---------|---------|---------|
| P1 | 8-10 | 6-12 | Holds 45-60s | 8-15 | 12-15 |
| P2 | 4-6 | 5-8 | Holds 30-45s + 8s max | 8-12 | 10-12 |
| P3 | 3-4 + explosive | 3-6 | Holds 20-30s + dynamic | 8-10 | 8-12 |

### PC-4: Tempo Requirements
| Phase | A Block Tempo | B Block Tempo | General Rule |
|-------|--------------|--------------|-------------|
| P1 | 3-4s eccentric, controlled | 3-5s eccentric | Time under tension focus |
| P2 | 2-3s eccentric, heavy | 2-4s eccentric | Strength focus |
| P3 | 1-2s eccentric, explosive concentric | 1-2s eccentric, explosive | Speed/power focus |

### PC-5: RPE Targets Per Phase
| Phase | A Block | B Block | C Block | D Block | E Block |
|-------|---------|---------|---------|---------|---------|
| P1 | 7 | 7-8 | 6-7 | 6-7 | 7 |
| P2 | 8-9 | 8-9 | 7-9 | 7-8 | 8 |
| P3 | 8-9 | 8-9 | 7-8 | 8-9 | 8-9 |
| Deload | 5-6 | 5-6 | 5-6 | 5-6 | 5-6 |

---

## PROGRESSION CONSTRAINTS

### PRG-1: Isometric Progression (C Block)
Phase 1 → Phase 2 → Phase 3:
- Yielding isometrics → Overcoming isometrics → Reactive isometrics
- PAILs/RAILs → Loaded stretches → Dynamic end-range
- This progression is MANDATORY. The AI cannot generate overcoming isometrics in Phase 1 or yielding-only in Phase 3.

### PRG-2: Core Progression (D Block)
Phase 1 → Phase 2 → Phase 3:
- Anti-movement (stability) → Loaded (strength) → Explosive (power)
- Dead Bug/Side Plank/Pallof → Ab Wheel/Copenhagen/TGU → Hanging Raises/Med Ball Slams/Dynamic Planks

### PRG-3: Nordic Curl Progression (B Block - B1 position)
Phase 1: Eccentric-only (3-5s lowering), hands to push back up
Phase 2: Full range with band-assisted concentric, reducing assistance weekly
Phase 3: Full concentric attempted unassisted
- This is in EVERY session's B Block. Non-negotiable for ACL prehab.

### PRG-4: Neck Progression (D Block - D4 position)
Phase 1: Isometric holds (hand/light band resistance, 10s each direction)
Phase 2: Dynamic reps (medium band, 8-10 each direction)
Phase 3: Heavy dynamic (heavy band/harness, 10-12 each direction, sport speed)
- In EVERY session. Non-negotiable for martial arts athletes.

### PRG-5: End-Range Progression (C Block)
Phase 1: Passive → active stretches (PAILs/RAILs, long holds)
Phase 2: Loaded stretches (hold weight in stretch position) + overcoming isos
Phase 3: Dynamic end-range (moving through full ROM under control) + maintenance

### PRG-6: Hypertrophy Progression (E Block)
Phase 1: 2 sets, light-moderate, mind-muscle connection
Phase 2: 3 sets, moderate-heavy, approach failure
Phase 3: 2 sets, intensity techniques (drop sets, supersets), maintain stimulus

### PRG-7: Weekly Load Progression (A Block)
Phase 1: +5-10lbs/week or reduce band assistance
Phase 2: +5lbs/week on working weight
Phase 3: Maintain heavy load, increase explosive intent
Deload weeks: 60-70% of peak week weight

---

## EXERCISE SELECTION CONSTRAINTS

### ES-1: Pull-to-Push Ratio
Minimum 3:2 across every session. The AI MUST count pulling vs pushing movements and verify the ratio before finalizing. Pulling includes: pull-ups, rows, face pulls, band pull-aparts. Pushing includes: presses, dips, push-ups.

### ES-2: Session Specificity
- Session A: Sagittal plane dominant (squat patterns, vertical pull)
- Session B: Frontal/rotational plane dominant (lateral patterns, horizontal pull)
- Session C: Posterior chain dominant (hip hinge, overhead press)
- Session D: Sport-specific (varies by phase)
- The AI must not generate a hip hinge as Session A's primary or a squat as Session C's primary.

### ES-3: No Exercise Duplication Across Sessions
No exercise may appear in more than one session within the same phase, EXCEPT:
- Nordic curl variants (mandatory in all B Blocks)
- F Block accessories (distributed per F-Block distribution rules)
- Warm-up movements (CARs, band pull-aparts are universal)

### ES-4: Accessory Distribution (F Block)
- Lower-emphasis days (Session A, C): Calf Raise + Tibialis Raise
- Upper-emphasis days (Session B, D): Dead Hang + Wrist Roller
- NEVER program all 4 accessories in one session unless Session D AND user has extra time

### ES-5: Equipment Constraints
The AI MUST check the user's equipment profile from the quiz and:
- Exclude any exercise requiring unavailable equipment
- Provide substitutions from the exercise substitution table
- If home gym: no cable exercises unless bands are available as substitute
- If no barbell: substitute DB or KB variants for all barbell movements

### ES-6: Injury Accommodations
The AI MUST check the user's injury profile and:
- Exclude any exercise flagged as contraindicated for their condition
- Apply ROM restrictions where specified
- Add prehab exercises for the relevant joint/area
- For ACL history: enforce Nordic curl inclusion, single-leg balance work, progressive plyometric introduction (no high-impact until Phase 3)

---

## WARM-UP CONSTRAINTS

### WU-1: Warm-Up Structure Per Phase
Phase 1: Foam Roll (5 min) → Movement Prep (5 min) → CARs (2 min) → Band Activation (2 min)
Phase 2: Foam Roll (3 min) → Movement Prep (4 min) → CARs (2 min) → Overcoming Isos (3 min) → Band Activation (2 min)
Phase 3: Foam Roll (2 min) → Movement Prep (3 min) → CARs (2 min) → Overcoming Isos (2 min) → Neural Activation/Plyos (3 min) → Band Activation (2 min)

### WU-2: Mandatory Warm-Up Elements
- CARs (hips + shoulders) in EVERY warm-up
- Band pull-aparts in EVERY warm-up
- Session-specific mobility drills matching the session's movement plane

---

## VALIDATION RULES

After generating a plan, the AI must self-check:

1. ☐ Every standard session has blocks A through F in order
2. ☐ Session D has the correct phase-specific structure
3. ☐ Deload weeks 4, 8, 12 have reduced volume (40-50%)
4. ☐ Nordic curls appear in every B Block
5. ☐ Neck work appears in every D Block
6. ☐ Pull-to-push ratio ≥ 3:2 in every session
7. ☐ F Block accessories are distributed (not repeated across all sessions)
8. ☐ Isometric progression follows: yielding → overcoming → reactive
9. ☐ Core progression follows: anti-movement → loaded → explosive
10. ☐ No equipment violations against user profile
11. ☐ No injury contraindications violated
12. ☐ Rep ranges match the phase prescription
13. ☐ Tempo prescriptions match the phase
14. ☐ RPE targets match the phase
15. ☐ E Block exercises vary by session (not identical across A, B, C)

If any check fails, the plan MUST be corrected before returning to the user.

