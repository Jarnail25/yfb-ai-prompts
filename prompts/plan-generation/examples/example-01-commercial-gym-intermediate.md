# Few-Shot Example 01 — Commercial Gym, Intermediate, No Injuries

Demonstrates: baseline session structure, all 6 blocks (A-F), correct pull:push ratio,
Nordic placement, F-block distribution, Phase 1 rep ranges and isometrics.

---

## Input Profile (Key Fields)

```json
{
  "persona_id": "example-01",
  "age": 32,
  "biological_sex": "male",
  "training_experience": "intermediate",
  "training_history": "3 years consistent training. Bro split. No periodization experience.",
  "goals": { "primary": "strength", "secondary": "fat_loss" },
  "injuries": [],
  "equipment": {
    "location": "commercial_gym",
    "available": ["barbell", "dumbbells", "cables", "machines", "pull_up_bar", "bench", "squat_rack", "hex_bar", "rings"]
  },
  "schedule": {
    "days_per_week": 3,
    "session_duration_minutes": 65,
    "preferred_days": ["monday", "wednesday", "friday"]
  },
  "body_composition": {
    "height_cm": 180,
    "weight_kg": 85,
    "body_fat_percent": 18
  }
}
```

---

## Expected Plan Output

> NOTE: Full 12-week plan would include all phases and weeks. This example shows
> Phase 1 Session A in complete detail, with Sessions B/C abbreviated and
> Phase 2/3 shown as progression deltas. Use this structure for ALL sessions.

```json
{
  "plan_metadata": {
    "plan_id": "example-01-plan",
    "user_id": "example-01-user",
    "generated_at": "2026-03-01T00:00:00Z",
    "methodology_version": "cressey-hybrid-v1",
    "duration_weeks": 12,
    "sessions_per_week": 3,
    "equipment_profile": {
      "location": "commercial_gym",
      "available": ["barbell", "dumbbells", "cables", "pull_up_bar", "bench", "squat_rack", "hex_bar", "rings"],
      "not_available": []
    },
    "injury_flags": [],
    "validation_checks": {
      "block_order_correct": true,
      "deload_weeks_present": true,
      "nordic_curl_every_session": true,
      "neck_work_every_session": true,
      "pull_push_ratio_met": true,
      "f_block_distributed": true,
      "isometric_progression_correct": true,
      "core_progression_correct": true,
      "no_equipment_violations": true,
      "no_injury_violations": true,
      "rep_ranges_match_phase": true,
      "e_block_varies_by_session": true
    }
  },

  "phases": [
    {
      "phase_number": 1,
      "phase_name": "Foundation",
      "weeks": { "start": 1, "end": 4, "deload_week": 4 },
      "goal": "Build structural tolerance, movement quality, and base strength. Introduce full 6-block session format.",
      "rep_range_primary": "8-10",
      "tempo_emphasis": "3-1-2-0 (3s eccentric, 1s pause, 2s concentric)",
      "rpe_range": "6-7",
      "isometric_type": "yielding",
      "core_emphasis": "anti-movement",
      "end_range_type": "passive-to-active",

      "sessions": [
        {
          "session_id": "A",
          "session_type": "Sagittal — Primary Strength + Vertical Pull",
          "movement_plane": "sagittal",
          "estimated_duration_minutes": 65,
          "pull_push_count": {
            "pull": 5,
            "push": 3,
            "ratio_met": true
          },
          "blocks": [
            {
              "block_id": "warm_up",
              "block_name": "Warm-Up",
              "purpose": "Foam rolling, movement prep, neural activation",
              "duration_minutes": 10,
              "exercises": [
                { "exercise_id": "WU1", "name": "Foam Roll T-Spine", "sets": 1, "reps": "60s", "tempo": "slow", "rpe": "5", "load_prescription": "BW", "rest_seconds": 0, "coaching_cue": "Pause on sticky spots. 3-4 holds." },
                { "exercise_id": "WU2", "name": "90/90 Hip Switch", "sets": 1, "reps": "8 each side", "tempo": "controlled", "rpe": "5", "load_prescription": "BW", "rest_seconds": 0, "coaching_cue": "Keep tall spine. Drive rear hip to floor actively." },
                { "exercise_id": "WU3", "name": "World's Greatest Stretch", "sets": 1, "reps": "5 each side", "tempo": "controlled", "rpe": "5", "load_prescription": "BW", "rest_seconds": 0, "coaching_cue": "Full hip drop on lunge, thoracic rotation on reach." },
                { "exercise_id": "WU4", "name": "Band Pull-Apart", "sets": 2, "reps": "15", "tempo": "2-1-2-0", "rpe": "5", "load_prescription": "Light band", "rest_seconds": 15, "coaching_cue": "Shoulder blades retract and depress. No upper trap." },
                { "exercise_id": "WU5", "name": "Banded Clamshell", "sets": 1, "reps": "12 each side", "tempo": "2-1-2-0", "rpe": "5", "load_prescription": "Light band", "rest_seconds": 15, "coaching_cue": "Pelvis stays stacked. Hip external rotation only, no pelvis tilt." }
              ]
            },
            {
              "block_id": "A",
              "block_name": "A Block — Primary Strength",
              "purpose": "Main compound lift + primary antagonist. Superset for efficiency.",
              "duration_minutes": 17,
              "rest_between_exercises": "90s after each superset",
              "exercises": [
                {
                  "exercise_id": "A1",
                  "name": "Bulgarian Split Squat",
                  "sets": 3,
                  "reps": "8-10 each leg",
                  "tempo": "3-1-2-0",
                  "rpe": "7",
                  "load_prescription": "Moderate DBs (aim for 8-10kg first session, progress weekly)",
                  "rest_seconds": 90,
                  "superset_with": "A2",
                  "coaching_cue": "Rear foot elevated on bench. Front shin vertical. Drive through full foot, not just toe.",
                  "movement_category": "squat",
                  "weekly_progression": [
                    { "week": 1, "load_adjustment": "Baseline week. Find working weight at RPE 6.", "notes": "Focus on form" },
                    { "week": 2, "load_adjustment": "+2kg DBs or same load with better control", "notes": null },
                    { "week": 3, "load_adjustment": "+2kg more. RPE should hit 7 by week 3.", "notes": null },
                    { "week": 4, "load_adjustment": "Deload: -40%. 2 sets × 6 reps at RPE 5.", "notes": "Recovery week" }
                  ],
                  "substitutions": [
                    { "name": "Rear-Foot Elevated Lunge (lower bench height)", "reason": "Balance limitation on first attempt" },
                    { "name": "Step-Up with KB", "reason": "Knee sensitivity" }
                  ]
                },
                {
                  "exercise_id": "A2",
                  "name": "Dead-Hang Pull-Up",
                  "sets": 3,
                  "reps": "6-8",
                  "tempo": "3-1-1-0",
                  "rpe": "7",
                  "load_prescription": "BW (add band assist if <6 reps available)",
                  "rest_seconds": 90,
                  "superset_with": "A1",
                  "coaching_cue": "Full dead hang start. Initiate with shoulder blade depression, not arm pull. Chin clears bar.",
                  "movement_category": "pull",
                  "weekly_progression": [
                    { "week": 1, "load_adjustment": "Baseline. Use band assist if needed.", "notes": null },
                    { "week": 2, "load_adjustment": "Aim for 1 more rep or reduce band tension.", "notes": null },
                    { "week": 3, "load_adjustment": "Same or +1 rep. RPE 7-8.", "notes": null },
                    { "week": 4, "load_adjustment": "Deload: 2 sets × 5 reps at RPE 5.", "notes": null }
                  ],
                  "substitutions": [
                    { "name": "Lat Pulldown (supinated grip)", "reason": "Cannot yet do BW pull-up" },
                    { "name": "Ring Row (feet elevated)", "reason": "No pull-up bar" }
                  ]
                }
              ]
            },
            {
              "block_id": "B",
              "block_name": "B Block — Secondary Strength + Nordics",
              "purpose": "Nordic curl (non-negotiable ACL prehab), pressing, and rotational work.",
              "duration_minutes": 13,
              "rest_between_exercises": "60s",
              "exercises": [
                {
                  "exercise_id": "B1",
                  "name": "Nordic Curl (Eccentric Phase 1)",
                  "sets": 3,
                  "reps": "4-6 eccentric only",
                  "tempo": "5-0-0-0 (5s lowering, catch with hands)",
                  "rpe": "7",
                  "load_prescription": "BW eccentric. Partner-assisted or anchor feet under bar.",
                  "rest_seconds": 60,
                  "coaching_cue": "Lock hips. Slow controlled descent. Catch with hands, push back up. This is THE hamstring injury prevention exercise.",
                  "movement_category": "pull",
                  "weekly_progression": [
                    { "week": 1, "load_adjustment": "3 sets × 4 reps. Focus on control.", "notes": null },
                    { "week": 2, "load_adjustment": "3 sets × 5 reps.", "notes": null },
                    { "week": 3, "load_adjustment": "3 sets × 6 reps.", "notes": null },
                    { "week": 4, "load_adjustment": "Deload: 2 sets × 3 reps.", "notes": null }
                  ]
                },
                {
                  "exercise_id": "B2",
                  "name": "Incline DB Press",
                  "sets": 3,
                  "reps": "8-10",
                  "tempo": "3-1-2-0",
                  "rpe": "7",
                  "load_prescription": "Moderate DBs",
                  "rest_seconds": 60,
                  "coaching_cue": "45-degree incline. Slight flare of elbows, not fully tucked. Full ROM — pause briefly at chest.",
                  "movement_category": "push"
                },
                {
                  "exercise_id": "B3",
                  "name": "Pallof Press (anti-rotation hold)",
                  "sets": 3,
                  "reps": "8 each side (3s hold each rep)",
                  "tempo": "1-3-1-0",
                  "rpe": "6",
                  "load_prescription": "Cable or band — light to moderate",
                  "rest_seconds": 60,
                  "coaching_cue": "Stagger stance perpendicular to anchor. Press and hold. ZERO rotation at spine. Brace deep.",
                  "movement_category": "rotation"
                }
              ]
            },
            {
              "block_id": "C",
              "block_name": "C Block — Isometric + End-Range (Yielding P1)",
              "purpose": "Passive-to-active end-range training, yielding isometrics, pistol squat progression.",
              "duration_minutes": 11,
              "rest_between_exercises": "30-45s",
              "exercises": [
                {
                  "exercise_id": "C1",
                  "name": "Ring-Assisted Pistol Squat (yielding)",
                  "sets": 3,
                  "reps": "5 each leg with 3s hold at bottom",
                  "tempo": "3-3-2-0",
                  "rpe": "6",
                  "load_prescription": "Ring assist (reduce assist each week)",
                  "rest_seconds": 45,
                  "coaching_cue": "Ring takes ~20% of load. Full ankle dorsiflexion. Sit into the bottom position — this is a yielding isometric. Control the return."
                },
                {
                  "exercise_id": "C2",
                  "name": "Hip 90/90 PAILs (External Rotation)",
                  "sets": 2,
                  "reps": "2 min passive + 1 min PAIL + 30s RAIL",
                  "tempo": "hold",
                  "rpe": "6",
                  "load_prescription": "BW",
                  "rest_seconds": 30,
                  "coaching_cue": "First 2 min: passive relaxation. PAIL: gradually push thigh INTO floor (external rotation effort). RAIL: try to lift thigh off floor (internal rotation). Maximum effort last 20s."
                },
                {
                  "exercise_id": "C3",
                  "name": "Lat Stretch with Breathing (passive)",
                  "sets": 2,
                  "reps": "60s each side",
                  "tempo": "hold",
                  "rpe": "5",
                  "load_prescription": "BW",
                  "rest_seconds": 30,
                  "coaching_cue": "Hang off rack, overhead grip. Allow shoulder to fully open. Deep exhales to deepen stretch. Not a hanging pull — pure passive stretch."
                }
              ]
            },
            {
              "block_id": "D",
              "block_name": "D Block — Core Circuit (Anti-Movement P1)",
              "purpose": "Anti-extension, anti-rotation, spinal extension, and isometric neck.",
              "duration_minutes": 9,
              "rest_between_exercises": "20-30s (circuit)",
              "exercises": [
                {
                  "exercise_id": "D1",
                  "name": "Dead Bug",
                  "sets": 3,
                  "reps": "8 each side (slow)",
                  "tempo": "4s lower, hold 1s",
                  "rpe": "6",
                  "load_prescription": "BW",
                  "rest_seconds": 20,
                  "coaching_cue": "Lower back PINNED to floor — no air gap. Opposite arm and leg extend simultaneously. Core breathes through the movement, not held breath."
                },
                {
                  "exercise_id": "D2",
                  "name": "Side Plank with Hip Abduction",
                  "sets": 3,
                  "reps": "30s each side",
                  "tempo": "hold",
                  "rpe": "6",
                  "load_prescription": "BW",
                  "rest_seconds": 20,
                  "coaching_cue": "Full body alignment — head to heel. Top hip abduction adds glute med demand. Don't let hips sag."
                },
                {
                  "exercise_id": "D3",
                  "name": "45° Back Extension (hold at top)",
                  "sets": 3,
                  "reps": "10 with 2s hold",
                  "tempo": "2-2-2-0",
                  "rpe": "6",
                  "load_prescription": "BW or light plate across chest",
                  "rest_seconds": 20,
                  "coaching_cue": "Neutral spine — NOT hyperextension. Hold at parallel. Squeeeze glutes and hamstrings at top. This trains spinal extensors isometrically."
                },
                {
                  "exercise_id": "D4",
                  "name": "Isometric Neck — 4-Way Series",
                  "sets": 1,
                  "reps": "10s each direction × 4 directions",
                  "tempo": "10s hold",
                  "rpe": "5",
                  "load_prescription": "Manual resistance (hand on head) or band",
                  "rest_seconds": 10,
                  "coaching_cue": "Flex, extend, lateral (both sides). Apply 40% max force against immovable resistance. This is a non-negotiable cervical strengthening inclusion every session.",
                  "movement_category": "isometric"
                }
              ]
            },
            {
              "block_id": "E",
              "block_name": "E Block — Hypertrophy (Session A: Biceps + Lateral Raise + Quad Accessory)",
              "purpose": "Accessory hypertrophy. Mind-muscle focus. Session A targets biceps, shoulders, quads.",
              "duration_minutes": 9,
              "rest_between_exercises": "45s",
              "exercises": [
                {
                  "exercise_id": "E1",
                  "name": "Incline DB Curl",
                  "sets": 2,
                  "reps": "12-15",
                  "tempo": "3-1-1-0",
                  "rpe": "7",
                  "load_prescription": "Light-moderate DBs",
                  "rest_seconds": 45,
                  "coaching_cue": "Full stretch at bottom on incline. Supinate at top. Slow eccentric. No swinging."
                },
                {
                  "exercise_id": "E2",
                  "name": "Cable Lateral Raise",
                  "sets": 2,
                  "reps": "12-15 each side",
                  "tempo": "2-1-2-0",
                  "rpe": "7",
                  "load_prescription": "Cable at lowest setting — light",
                  "rest_seconds": 45,
                  "coaching_cue": "Slight forward lean. Lead with elbow, not hand. Full ROM — arm to 90° or slightly above."
                },
                {
                  "exercise_id": "E3",
                  "name": "Leg Extension (slow eccentric)",
                  "sets": 2,
                  "reps": "12-15",
                  "tempo": "2-1-4-0",
                  "rpe": "7",
                  "load_prescription": "Machine — moderate",
                  "rest_seconds": 45,
                  "coaching_cue": "Slow 4s eccentric. Full contraction at top. Quad isolation — control the drop."
                }
              ]
            },
            {
              "block_id": "F",
              "block_name": "F Block — Accessory: Session A (Calf + Tibialis)",
              "purpose": "Tendon health. Calf/tibialis pair for Session A (sagittal emphasis). Daily-trainable frequency.",
              "duration_minutes": 6,
              "rest_between_exercises": "30s",
              "exercises": [
                {
                  "exercise_id": "F1",
                  "name": "Single-Leg Calf Raise (slow eccentric)",
                  "sets": 2,
                  "reps": "12-15 each leg",
                  "tempo": "2-1-4-0",
                  "rpe": "6",
                  "load_prescription": "BW or light DB — focus on ROM",
                  "rest_seconds": 30,
                  "coaching_cue": "Full plantarflexion at top. 4s controlled lowering below neutral. Full stretch at bottom. Calf tendon health over load."
                },
                {
                  "exercise_id": "F2",
                  "name": "Tibialis Raise (against wall)",
                  "sets": 2,
                  "reps": "15",
                  "tempo": "2-1-2-0",
                  "rpe": "6",
                  "load_prescription": "BW or band at toe",
                  "rest_seconds": 30,
                  "coaching_cue": "Heels to wall. Dorsiflex toes UP as far as possible. Slow return. Prevents shin splints, improves ankle mobility."
                }
              ]
            }
          ]
        },

        {
          "session_id": "B",
          "session_type": "Frontal/Rotational — Secondary Strength + Horizontal Pull",
          "movement_plane": "frontal",
          "estimated_duration_minutes": 65,
          "pull_push_count": { "pull": 5, "push": 3, "ratio_met": true },
          "blocks": [
            { "block_id": "warm_up", "block_name": "Warm-Up", "notes": "Same warm-up protocol as Session A" },
            {
              "block_id": "A",
              "block_name": "A Block — Lateral Squat + Horizontal Row",
              "exercises": [
                { "exercise_id": "A1", "name": "Cossack Squat", "sets": 3, "reps": "6-8 each side", "tempo": "3-1-2-0", "rpe": "7", "load_prescription": "BW or light KB", "rest_seconds": 90, "superset_with": "A2", "coaching_cue": "Full ankle mobility required. Sit deep. Groin stretch on extended leg. Add load only when depth is solid.", "movement_category": "squat" },
                { "exercise_id": "A2", "name": "Barbell Bent-Over Row (pronated)", "sets": 3, "reps": "8-10", "tempo": "2-1-3-0", "rpe": "7", "load_prescription": "Moderate barbell", "rest_seconds": 90, "superset_with": "A1", "coaching_cue": "Hip hinge to ~45°. Pull to lower sternum. Slow 3s eccentric. Row with elbows, not arms.", "movement_category": "pull" }
              ]
            },
            {
              "block_id": "B",
              "block_name": "B Block — Nordic + Floor Press + Woodchop",
              "exercises": [
                { "exercise_id": "B1", "name": "Nordic Curl (Eccentric Phase 1)", "sets": 3, "reps": "4-6 eccentric", "tempo": "5-0-0-0", "rpe": "7", "load_prescription": "BW", "rest_seconds": 60, "coaching_cue": "Same as Session A — Nordic in B1 every session without exception.", "movement_category": "pull" },
                { "exercise_id": "B2", "name": "DB Floor Press", "sets": 3, "reps": "8-10", "tempo": "3-1-2-0", "rpe": "7", "load_prescription": "Moderate DBs", "rest_seconds": 60, "coaching_cue": "Upper arms rest on floor at bottom — full stretch. Press to lockout.", "movement_category": "push" },
                { "exercise_id": "B3", "name": "Cable Woodchop (high-to-low)", "sets": 3, "reps": "8 each side", "tempo": "2-1-2-0", "rpe": "6", "load_prescription": "Light cable", "rest_seconds": 60, "coaching_cue": "Rotate through thoracic spine, not lower back. Keep hips facing forward. Pull through full arc.", "movement_category": "rotation" }
              ]
            },
            { "block_id": "C", "block_name": "C Block — Isometrics + End-Range", "notes": "Same structure as Session A C Block. Substitute Hip 90/90 with Couch Stretch." },
            { "block_id": "D", "block_name": "D Block — Core Circuit", "notes": "Same format. D1: Pallof Hold. D2: Copenhagen Plank. D3: Back Extension. D4: Neck 4-Way." },
            { "block_id": "E", "block_name": "E Block — Session B: Triceps + Rear Delt + Traps", "notes": "E1: Cable Overhead Tricep Extension 2×12-15. E2: Face Pull 2×12-15. E3: DB Shrug 2×15." },
            { "block_id": "F", "block_name": "F Block — Session B: Dead Hang + Wrist Roller", "notes": "F1: Dead Hang 2×20-30s. F2: Wrist Roller 2×3 rolls each direction. 30s rest." }
          ]
        },

        {
          "session_id": "C",
          "session_type": "Posterior Chain — Hip Hinge + Overhead Press",
          "movement_plane": "sagittal (posterior emphasis)",
          "estimated_duration_minutes": 65,
          "pull_push_count": { "pull": 5, "push": 3, "ratio_met": true },
          "blocks": [
            { "block_id": "warm_up", "block_name": "Warm-Up", "notes": "Same warm-up protocol as Session A" },
            {
              "block_id": "A",
              "block_name": "A Block — Hex Bar Deadlift + Overhead Press",
              "exercises": [
                { "exercise_id": "A1", "name": "Hex Bar Deadlift", "sets": 3, "reps": "6-8", "tempo": "3-1-2-0", "rpe": "7", "load_prescription": "Moderate-heavy barbell in hex bar", "rest_seconds": 90, "superset_with": "A2", "coaching_cue": "Hip hinge — sit back, brace, drive through floor. Neutral spine. No lower back rounding. Phase 1 focuses on position and tension, not max load.", "movement_category": "hinge" },
                { "exercise_id": "A2", "name": "DB Overhead Press (seated or standing)", "sets": 3, "reps": "8-10", "tempo": "3-1-2-0", "rpe": "7", "load_prescription": "Moderate DBs", "rest_seconds": 90, "superset_with": "A1", "coaching_cue": "Slight forward lean of torso. Press in line with ears, not directly overhead. Control the eccentric.", "movement_category": "push" }
              ]
            },
            {
              "block_id": "B",
              "block_name": "B Block — Nordic + RDL + Landmine Rotation",
              "exercises": [
                { "exercise_id": "B1", "name": "Nordic Curl (Eccentric Phase 1)", "sets": 3, "reps": "4-6 eccentric", "tempo": "5-0-0-0", "rpe": "7", "load_prescription": "BW", "rest_seconds": 60, "coaching_cue": "Nordic curl — non-negotiable every session. Same execution.", "movement_category": "pull" },
                { "exercise_id": "B2", "name": "Single-Leg RDL", "sets": 3, "reps": "8-10 each leg", "tempo": "3-1-2-0", "rpe": "7", "load_prescription": "Light-moderate KB or DB", "rest_seconds": 60, "coaching_cue": "Hip hinge on one leg. Opposite leg floats back. Spine neutral, hip drive to stand. Balance challenge is intentional.", "movement_category": "hinge" },
                { "exercise_id": "B3", "name": "Landmine Rotation", "sets": 3, "reps": "8 each side", "tempo": "2-1-2-0", "rpe": "6", "load_prescription": "Light barbell in landmine", "rest_seconds": 60, "coaching_cue": "Rotate through thoracic spine. Keep hips facing forward. The arc should be smooth — control the deceleration.", "movement_category": "rotation" }
              ]
            },
            { "block_id": "C", "block_name": "C Block", "notes": "Same structure. Emphasise hip flexor and hamstring end-range: Couch Stretch PAILs + SL Romanian Stretch." },
            { "block_id": "D", "block_name": "D Block", "notes": "D1: Ab Wheel Rollout (knees). D2: Side Plank. D3: Back Extension. D4: Neck 4-Way." },
            { "block_id": "E", "block_name": "E Block — Session C: Rows + Glutes + Lats", "notes": "E1: Seated Cable Row 2×12-15. E2: Hip Thrust 2×12-15. E3: Straight-Arm Pulldown 2×12-15." },
            { "block_id": "F", "block_name": "F Block — Session C: Calf + Tibialis", "notes": "Same as Session A: SL Calf Raise + Tibialis Raise. 2×12-15." }
          ]
        }
      ]
    },

    {
      "phase_number": 2,
      "phase_name": "Accumulation",
      "weeks": { "start": 5, "end": 8, "deload_week": 8 },
      "goal": "Increase intensity and volume. Transition to overcoming isometrics.",
      "rep_range_primary": "4-6",
      "tempo_emphasis": "2-1-1-0 (strength tempo — faster concentric intent)",
      "rpe_range": "8-9",
      "isometric_type": "overcoming",
      "core_emphasis": "loaded",
      "end_range_type": "loaded",
      "progression_deltas": {
        "A_block": "Increase load 5-10% from P1 final week. Add 1 set (4 total). Reduce reps to 4-6.",
        "B_block": "Nordic: progress to full concentric (push up through top). Load: +10% across board.",
        "C_block": "Yielding → Overcoming. Replace PAILs with 8s max-effort press-outs. Loaded stretches (DB in bottom of RDL hold).",
        "D_block": "Anti-movement → Loaded. Add AB Wheel, Copenhagen Plank, TGU.",
        "E_block": "Add 1 set (3 total). Closer to failure. Increase load 10%.",
        "F_block": "Add band resistance to Calf Raise. Dead Hang → Weighted Dead Hang."
      }
    },

    {
      "phase_number": 3,
      "phase_name": "Realization",
      "weeks": { "start": 9, "end": 12, "deload_week": 12 },
      "goal": "Peak strength expression and power. Contrast pairs in A Block. Reactive isometrics.",
      "rep_range_primary": "3-4",
      "tempo_emphasis": "3-1-X-0 (explosive concentric intent — X = max velocity)",
      "rpe_range": "8-9",
      "isometric_type": "reactive",
      "core_emphasis": "explosive",
      "end_range_type": "dynamic-maintenance",
      "progression_deltas": {
        "A_block": "Contrast pairs: A1 heavy compound (3-4 reps) → A2 explosive (e.g., BSS → Box Jump, Row → Med Ball Slam). 60-90s between.",
        "B_block": "Nordic: full eccentric + concentric. Add resistance (band or loaded vest).",
        "C_block": "Overcoming → Reactive. Dynamic end-range pistols. Continuous articular rotations (CARs).",
        "D_block": "Explosive: Med Ball Slams, Hanging Raises, L-Sit holds. Neck: heavier resistance.",
        "E_block": "Drop sets or supersets. 2 sets × 8-12. Closer to failure.",
        "F_block": "Heavy weighted Calf Raise. Explosive tibialis. Dead Hang with weight."
      }
    }
  ],

  "warm_ups": {
    "phase_1": {
      "total_duration_minutes": 10,
      "sections": [
        { "name": "Tissue Prep (Foam Roll)", "duration_minutes": 3, "exercises": [
          { "name": "Foam Roll T-Spine", "sets": 1, "reps": "60s" },
          { "name": "Foam Roll Glutes", "sets": 1, "reps": "45s each" }
        ]},
        { "name": "Movement Prep", "duration_minutes": 4, "exercises": [
          { "name": "90/90 Hip Switch", "sets": 1, "reps": "8 each" },
          { "name": "World's Greatest Stretch", "sets": 1, "reps": "5 each" }
        ]},
        { "name": "Neural Activation", "duration_minutes": 3, "exercises": [
          { "name": "Band Pull-Apart", "sets": 2, "reps": "15" },
          { "name": "Banded Clamshell", "sets": 1, "reps": "12 each" }
        ]}
      ]
    },
    "phase_2": {
      "total_duration_minutes": 10,
      "sections": [
        { "name": "Tissue Prep", "duration_minutes": 2, "exercises": [
          { "name": "Foam Roll (targeted — problem areas only)", "sets": 1, "reps": "45s each" }
        ]},
        { "name": "Movement Prep", "duration_minutes": 4, "exercises": [
          { "name": "90/90 Hip Switch", "sets": 1, "reps": "6 each" },
          { "name": "World's Greatest Stretch", "sets": 1, "reps": "4 each" },
          { "name": "Deep Squat Hold with Breathing", "sets": 1, "reps": "60s" }
        ]},
        { "name": "Neural Activation (heavier)", "duration_minutes": 4, "exercises": [
          { "name": "Band Pull-Apart", "sets": 2, "reps": "15" },
          { "name": "Explosive Glute Bridge", "sets": 2, "reps": "8" }
        ]}
      ]
    },
    "phase_3": {
      "total_duration_minutes": 8,
      "sections": [
        { "name": "Tissue Prep (brief)", "duration_minutes": 2, "exercises": [
          { "name": "Foam Roll (only essential areas)", "sets": 1, "reps": "30s each" }
        ]},
        { "name": "Power Prep", "duration_minutes": 6, "exercises": [
          { "name": "World's Greatest Stretch", "sets": 1, "reps": "4 each" },
          { "name": "Explosive Hip Bridge", "sets": 2, "reps": "8" },
          { "name": "Low Box Jump (sub-maximal)", "sets": 2, "reps": "3" }
        ]}
      ]
    }
  },

  "deload_protocol": {
    "volume_reduction_percent": 45,
    "intensity_percent_of_peak": 65,
    "rpe_cap": 6,
    "blocks_to_reduce": ["A", "B", "E"],
    "blocks_to_maintain": ["C", "D", "warm_up"],
    "notes": "Deload weeks are weeks 4, 8, and 12. Reduce sets by 1, drop reps 20%, cap RPE at 6. C Block and D Block maintained at full volume — mobility and core work does not regress on deload."
  },

  "readiness_assessment": {
    "factors": [
      { "name": "Sleep quality", "scale_min": 1, "scale_max": 10 },
      { "name": "Energy level", "scale_min": 1, "scale_max": 10 },
      { "name": "Motivation", "scale_min": 1, "scale_max": 10 },
      { "name": "Muscle soreness", "scale_min": 1, "scale_max": 10 },
      { "name": "Joint stiffness", "scale_min": 1, "scale_max": 10 }
    ],
    "thresholds": {
      "train_as_planned": "Average ≥ 6",
      "reduce_rpe_1": "Average 4-5.9 — reduce all RPE targets by 1 point",
      "reduce_rpe_2": "Average 2.5-3.9 — reduce RPE by 2, drop to 2 sets main lifts",
      "active_recovery_only": "Average < 2.5 — C Block and walking only"
    }
  }
}
```
