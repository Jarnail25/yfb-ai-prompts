# Exercise Selection Rules

Rules for selecting exercises based on user profile data. The plan generation AI MUST follow these constraints when choosing exercises for each block and session type.

---

## 1. Equipment Mapping

Only select exercises the user can perform with their available equipment. If an exercise requires equipment the user does not have, it MUST NOT appear in the plan.

### Equipment Tags
Each exercise in the exercise bank has one or more equipment tags. Match against the user's `equipment` array from the quiz.

| Equipment Tag | Quiz Value | Notes |
|--------------|-----------|-------|
| `bodyweight` | Always available | No equipment needed |
| `dumbbells` | "dumbbells" | Adjustable or fixed |
| `barbell` | "barbell" | Requires plates; check if rack available |
| `kettlebells` | "kettlebells" | |
| `pull_up_bar` | "pull-up bar" | Includes doorframe and wall-mounted |
| `bench` | "bench" | Flat or adjustable |
| `squat_rack` | "squat rack" | Implies barbell station |
| `cables` | "cables" | Cable machine or functional trainer |
| `bands` | "resistance bands" | Light/medium/heavy |
| `rings` | "rings" | Gymnastic rings |
| `cardio_machine` | "cardio machine" | Treadmill, bike, rower, etc. |
| `foam_roller` | "foam roller" | For warm-up only |
| `trx` | "TRX/suspension trainer" | |
| `landmine` | "barbell" + "squat rack" | Barbell in corner or landmine attachment |
| `med_ball` | "medicine ball" | For neural activation and core work |

### Minimum Equipment Plans
If a user has ONLY bodyweight:
- Block A: Pistol squat progressions, push-up progressions, Nordic curl progressions
- Block B: Single-leg hip thrusts, pike push-ups, bodyweight rows (using table/TRX if available)
- Block C: Isometric holds (wall sit, plank, dead hang if bar available)
- Block D: Hollow body, dead bugs, mountain climbers

If a user has bodyweight + dumbbells + bench:
- Full plan is achievable with DB substitutions for barbell movements
- DB Romanian deadlift instead of barbell RDL
- DB goblet squat instead of front squat
- DB row instead of barbell row
- DB bench press instead of barbell bench

---

## 2. Experience Level Adjustments

### Beginner (< 6 months consistent training)
- Limit exercise variety: 4-5 unique exercises per session (fewer to master form)
- No complex Olympic lifts or advanced plyometrics
- No single-leg barbell work (DB only for unilateral)
- No heavy isometric overcoming work until Phase 2
- Nordic curls: always eccentric-only with band assist or partner assist
- Default tempo: 3-1-2-0 (slow and controlled)
- RPE ceiling: 7 (never prescribe RPE 8-9 in Phase 1)
- Add "form focus" coaching cue to every exercise

### Intermediate (6 months - 2 years consistent)
- Standard exercise selection per methodology
- Can introduce moderate plyometrics in Phase 3 warm-up
- Nordic curls: eccentric → full range across phases
- RPE range per methodology defaults

### Advanced (2+ years consistent or competitive athlete)
- Full exercise palette including complex movements
- Can include barbell back squats if requested and no contraindications
- Olympic lift variations if sport demands it
- Reactive plyometrics in Phase 3
- Cluster sets and wave loading in Phase 3

---

## 3. Body Type and Anthropometry

### Tall Users (6'0" / 183cm+)
- Prioritize: trap bar deadlift over conventional, goblet squat over back squat
- Elevated heels for squat variations (note in coaching cue)
- Longer rest periods for compound movements (+15-30s)
- Avoid: movements with extreme ROM demands unless mobility confirmed
- Note: "Tall athletes may need stance/grip width adjustments" as coaching cue

### Desk Workers (sedentary job, 6+ hours sitting)
- ALWAYS include in warm-up: hip flexor stretch, thoracic extension, glute activation
- Prioritize: pull exercises, hip extension work, thoracic mobility
- Avoid: excessive seated exercises (prefer standing/half-kneeling alternatives)
- Block C: emphasize hip flexor PAILs/RAILs and thoracic end-range
- Add postural cue: "Shoulders back and down, chest up" to pulling exercises

### Age 40+ Adjustments
- Extend warm-up by 2-3 minutes
- Foundation phase: add 1 extra week
- Reduce plyometric intensity (box jump height, landing impact)
- Increase rest periods by 15-30s across all blocks
- Emphasize: joint-friendly alternatives (e.g., landmine press over strict overhead press)
- If hormonal concerns flagged: note "compound movements for hormonal optimization" in plan notes

### Age 55+ Adjustments
- All 40+ adjustments PLUS:
- Reduce peak RPE to 7-8 (never 9)
- Balance work in every warm-up (single-leg stance, tandem walk)
- No explosive plyometrics; replace with controlled power (e.g., MB chest pass instead of clap push-up)
- Longer deload weeks (reduce to 30-40% volume)

---

## 4. Goal-Based Exercise Priority

### Fat Loss
- Higher metabolic demand: prefer compound over isolation
- Block D: add conditioning finisher (battle ropes, sled push, bike sprint) if equipment allows
- Shorten rest periods by 15s across Blocks B and C
- Superset density: maximize supersets in Blocks B and C

### Muscle Gain (Hypertrophy)
- Higher volume in Phase 2 (5 sets for primary movements)
- Include isolation accessories: curls, lateral raises, calf raises as Block B add-ons
- Tempo emphasis: 3-1-1-0 with controlled eccentrics
- Rest periods: standard per methodology (muscle needs recovery between sets)

### Athletic Performance
- Power development in Phase 3 (explosive tempo, plyometrics)
- Sport-specific movement patterns in Block B
- Neural activation in warm-up uses sport-relevant movements
- Conditioning work mimics sport energy systems (intermittent for team sports, sustained for endurance)

### Longevity / General Health
- Balanced approach across all movement planes
- Emphasize Block C (mobility, end-range, isometrics) — never abbreviate
- Include balance and proprioception work in warm-up
- Moderate intensity throughout (peak RPE 7-8)

### Rehab / Pain-Free Movement
- Defer to injury protocols document entirely
- Reduce overall volume by 20%
- Extend Phase 1 by 1-2 weeks
- Every exercise must have a "pain-free alternative" coaching cue
- If pain > 3/10 during any movement, coaching cue: "Stop and substitute"

---

## 5. Session Type Exercise Pools

### Session A (Sagittal Plane)
**Block A options:** Front squat, goblet squat, trap bar deadlift, Bulgarian split squat (heavy), reverse lunge (heavy)
**Block B options:** Bench press/DB press + barbell row, push-up variation + inverted row, landmine press + cable row, walking lunges + face pulls
**Block C options:** Wall sit iso + hamstring PAILs/RAILs, split squat iso hold + shoulder end-range, dead hang + hip flexor stretch
**Block D options:** Dead bugs, Pallof press, plank variations → woodchops, MB slams → hanging leg raises, rotational throws

### Session B (Frontal/Rotational)
**Block A options:** Lateral lunge (heavy), Cossack squat, landmine press, single-arm DB press
**Block B options:** Cable rotation + single-arm row, lateral raise + band pull-apart, Copenhagen plank + Turkish get-up prep, lateral sled drag + rotational cable press
**Block C options:** Adductor iso + thoracic rotation PAILs, side plank iso + hip 90/90 end-range, lateral wall sit + shoulder sleeper stretch
**Block D options:** Pallof press rotations, cable woodchops, lateral medicine ball throws → rotational slam, side plank with rotation

### Session C (Posterior Chain)
**Block A options:** Romanian deadlift, hip thrust (barbell or DB), single-leg RDL, sumo deadlift, good morning
**Block B options:** Pull-up/chin-up + Nordic curl, cable pull-through + face pull, glute-ham raise + band pull-apart, reverse hyper + inverted row
**Block C options:** Hamstring iso (Nordic hold) + hip end-range PAILs, glute bridge iso + ankle dorsiflexion end-range, single-leg hip thrust iso + spinal decompression hang
**Block D options:** Dead bugs, reverse crunches, bird dogs → weighted carries, suitcase carry, farmer walks → hanging knee/leg raises

---

## 6. Exercise Substitution Rules

When an exercise cannot be performed (equipment, injury, skill level), substitute using this priority:

1. **Same movement pattern, same equipment** (e.g., barbell RDL → barbell good morning)
2. **Same movement pattern, different equipment** (e.g., barbell RDL → DB RDL)
3. **Similar movement pattern, available equipment** (e.g., barbell RDL → cable pull-through)
4. **Regression of the same exercise** (e.g., pull-up → band-assisted pull-up → lat pulldown → DB row)

Never substitute a pull with a push or vice versa. The pull:push ratio must be maintained.
