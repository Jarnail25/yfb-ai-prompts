# Few-Shot Example 02 — Home Gym, Beginner, Lower Back Sensitivity

Demonstrates: equipment substitutions (no barbell, minimal gear), injury
modifications (lower back — avoid loaded spinal flexion, heavy bilateral hinging),
beginner load prescriptions, technique-first progression.

---

## Input Profile (Key Fields)

```json
{
  "persona_id": "example-02",
  "age": 28,
  "biological_sex": "female",
  "training_experience": "beginner",
  "training_history": "Some gym experience, nothing consistent. Last trained 8 months ago.",
  "goals": { "primary": "fat_loss", "secondary": "strength", "tertiary": "posture" },
  "injuries": [
    {
      "location": "lower_back",
      "type": "recurring ache — worse with prolonged sitting and heavy deadlifts",
      "severity": "mild",
      "contraindicated_movements": ["heavy_bilateral_deadlift", "loaded_spinal_flexion", "heavy_good_morning"],
      "required_prehab": ["glute_activation", "hip_flexor_lengthening", "bird_dog", "mcgill_big_3"]
    }
  ],
  "equipment": {
    "location": "home_gym",
    "available": ["adjustable_dumbbells", "resistance_bands", "pull_up_bar", "bench", "yoga_mat"],
    "not_available": ["barbell", "squat_rack", "cables", "machines", "hex_bar"]
  },
  "schedule": {
    "days_per_week": 3,
    "session_duration_minutes": 45,
    "preferred_days": ["tuesday", "thursday", "saturday"]
  }
}
```

---

## Key Decision Points (Why the Plan Looks This Way)

1. **No bilateral heavy hinging** → A Block Session C uses SL RDL + Glute Bridge series instead of Hex Bar DL
2. **No barbell** → All pressing and pulling use DBs and bands
3. **Lower back prehab mandatory** → Warm-up includes Bird Dog + McGill Big 3 every session
4. **Beginner load prescription** → Phase 1 all at RPE 6, not 7. Technique weeks before load weeks.
5. **45-minute constraint** → F Block is abbreviated (1 exercise per session, not 2)
6. **Beginner Nordic progressions** → Start with foot-elevated isometric, not full eccentric

---

## Expected Plan Output (Phase 1, Session A — Full Detail)

```json
{
  "plan_metadata": {
    "plan_id": "example-02-plan",
    "methodology_version": "cressey-hybrid-v1",
    "duration_weeks": 12,
    "sessions_per_week": 3,
    "equipment_profile": {
      "location": "home_gym",
      "available": ["adjustable_dumbbells", "resistance_bands", "pull_up_bar", "bench", "yoga_mat"],
      "not_available": ["barbell", "squat_rack", "cables", "machines", "hex_bar"]
    },
    "injury_flags": [
      {
        "location": "lower_back",
        "type": "recurring ache",
        "severity": "mild",
        "contraindicated_movements": ["heavy_bilateral_deadlift", "loaded_spinal_flexion", "heavy_good_morning"],
        "required_prehab": ["glute_activation", "hip_flexor_lengthening", "bird_dog", "mcgill_big_3"]
      }
    ],
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
      "goal": "Build movement quality, glute and hip strength to offload lower back. Establish full session structure tolerance.",
      "rep_range_primary": "10-12",
      "tempo_emphasis": "3-1-2-0 (slow eccentrics to reinforce position)",
      "rpe_range": "5-6",
      "isometric_type": "yielding",
      "core_emphasis": "anti-movement",
      "end_range_type": "passive-to-active",

      "sessions": [
        {
          "session_id": "A",
          "session_type": "Sagittal — Split Squat + Pull-Up (or Band Pull)",
          "movement_plane": "sagittal",
          "estimated_duration_minutes": 45,
          "pull_push_count": { "pull": 4, "push": 2, "ratio_met": true },
          "blocks": [
            {
              "block_id": "warm_up",
              "block_name": "Warm-Up (Lower Back Prehab Priority)",
              "purpose": "Lower back prehab mandatory every session per injury protocol. McGill Big 3 is non-negotiable.",
              "duration_minutes": 8,
              "exercises": [
                { "exercise_id": "WU1", "name": "Bird Dog", "sets": 2, "reps": "8 each side (3s hold)", "tempo": "controlled", "rpe": "4", "load_prescription": "BW", "rest_seconds": 10, "coaching_cue": "Brace core before movement. Opposite arm + leg extend — no rotation. 3s hold at full extension. THIS IS LOWER BACK PREHAB — do not rush." },
                { "exercise_id": "WU2", "name": "McGill Curl-Up", "sets": 2, "reps": "5 each side (8s hold)", "tempo": "hold", "rpe": "4", "load_prescription": "BW", "rest_seconds": 10, "coaching_cue": "Hand under lumbar spine. Curl ONLY the head and neck — NOT a crunch. Maintains lumbar curve. Isometric abdominal activation." },
                { "exercise_id": "WU3", "name": "Side Plank (knees bent, beginner)", "sets": 1, "reps": "20s each side", "tempo": "hold", "rpe": "4", "load_prescription": "BW", "rest_seconds": 10, "coaching_cue": "Knee version — builds to full side plank over weeks. Hips forward, not dropped. This completes the McGill Big 3." },
                { "exercise_id": "WU4", "name": "Hip Flexor Lunge Stretch", "sets": 1, "reps": "45s each side", "tempo": "hold", "rpe": "4", "load_prescription": "BW", "rest_seconds": 15, "coaching_cue": "Lower back injury link: tight hip flexors overload lumbar. Gentle anterior pelvic tilt correction — tuck tailbone slightly in this stretch." },
                { "exercise_id": "WU5", "name": "Glute Bridge (activation)", "sets": 2, "reps": "10 with 3s hold at top", "tempo": "1-3-1-0", "rpe": "4", "load_prescription": "BW", "rest_seconds": 10, "coaching_cue": "Squeeze glutes hard at top. Weak glutes = lower back overload. This is activation, not training — feel the glute, not the hamstring." }
              ]
            },
            {
              "block_id": "A",
              "block_name": "A Block — Split Squat + Band Pull",
              "purpose": "Primary strength compound. Pull-up substituted with band row (no lat pulldown at home).",
              "duration_minutes": 12,
              "rest_between_exercises": "90s",
              "exercises": [
                {
                  "exercise_id": "A1",
                  "name": "Split Squat (front foot elevated on bench)",
                  "sets": 3,
                  "reps": "10-12 each leg",
                  "tempo": "3-1-2-0",
                  "rpe": "6",
                  "load_prescription": "BW weeks 1-2, light DBs weeks 3-4",
                  "rest_seconds": 90,
                  "superset_with": "A2",
                  "coaching_cue": "Front foot on bench edge, step back to split. Lower knee slowly toward floor. Drive through front heel to stand. Spine neutral throughout — this leg pattern protects the lower back vs bilateral squat.",
                  "movement_category": "squat",
                  "weekly_progression": [
                    { "week": 1, "load_adjustment": "BW only. Focus on depth and balance.", "notes": "Beginner: form first" },
                    { "week": 2, "load_adjustment": "BW + aim for 12 reps each side comfortably.", "notes": null },
                    { "week": 3, "load_adjustment": "Add 2-4kg DBs if balance is solid.", "notes": null },
                    { "week": 4, "load_adjustment": "Deload: BW only. 2 sets × 8.", "notes": null }
                  ]
                },
                {
                  "exercise_id": "A2",
                  "name": "Band Assisted Pull-Up (or Banded Row to bar)",
                  "sets": 3,
                  "reps": "8-10",
                  "tempo": "3-1-2-0",
                  "rpe": "6",
                  "load_prescription": "Heavy band assist for pull-up, or horizontal band row using pull-up bar",
                  "rest_seconds": 90,
                  "superset_with": "A1",
                  "coaching_cue": "If pull-ups not possible: hook band over pull-up bar, grab ends, lean back 45°, row up. This replicates the vertical pull pattern with home gym equipment.",
                  "movement_category": "pull"
                }
              ]
            },
            {
              "block_id": "B",
              "block_name": "B Block — Nordic Isometric + Band Press + Band Pallof",
              "duration_minutes": 11,
              "exercises": [
                {
                  "exercise_id": "B1",
                  "name": "Nordic Curl — Foot Elevated Isometric Hold (Beginner Regression)",
                  "sets": 3,
                  "reps": "5s hold at 30° lean × 5 reps",
                  "tempo": "hold",
                  "rpe": "6",
                  "load_prescription": "BW — feet anchored under bench or sofa",
                  "rest_seconds": 60,
                  "coaching_cue": "BEGINNER REGRESSION: Cannot do full Nordic yet. Hook feet under sofa/bench. Lock hips. Lean forward 30°, hold 5s, return. Build this isometric strength first before the full eccentric version.",
                  "movement_category": "pull"
                },
                {
                  "exercise_id": "B2",
                  "name": "DB Floor Press",
                  "sets": 3,
                  "reps": "10-12",
                  "tempo": "3-1-2-0",
                  "rpe": "6",
                  "load_prescription": "Light-moderate DBs",
                  "rest_seconds": 60,
                  "coaching_cue": "Floor press is IDEAL for this injury profile — it naturally limits ROM to a safe range and removes shoulder strain of full bench. Lie on mat, press DBs up from floor level.",
                  "movement_category": "push"
                },
                {
                  "exercise_id": "B3",
                  "name": "Band Pallof Press (anti-rotation isometric)",
                  "sets": 3,
                  "reps": "6 each side (3s hold each)",
                  "tempo": "1-3-1-0",
                  "rpe": "5",
                  "load_prescription": "Band anchored to pole, door frame, or heavy furniture",
                  "rest_seconds": 60,
                  "coaching_cue": "Band anchored at chest height. Press out and hold — resist rotation. This trains the core to protect the lower back under lateral load. Perfect for lower back rehab.",
                  "movement_category": "rotation"
                }
              ]
            },
            {
              "block_id": "C",
              "block_name": "C Block — Hip Mobility + Yielding Isometrics",
              "duration_minutes": 7,
              "exercises": [
                {
                  "exercise_id": "C1",
                  "name": "90/90 Hip Switch with PAILs (passive to active)",
                  "sets": 2,
                  "reps": "2 min passive + 1 min PAIL",
                  "rpe": "5",
                  "load_prescription": "BW",
                  "rest_seconds": 30,
                  "coaching_cue": "Passive: let hips relax fully into position. PAIL: gradually push thigh into floor (external rotation). Lower back injury = tight hips. This directly targets root cause."
                },
                {
                  "exercise_id": "C2",
                  "name": "Assisted Pistol Squat Hold (yielding isometric, TRX/band)",
                  "sets": 3,
                  "reps": "5 each leg, 3s hold at bottom",
                  "rpe": "5",
                  "load_prescription": "Band from door frame for support",
                  "rest_seconds": 30,
                  "coaching_cue": "Beginner version with band support. Sit into bottom position — focus is ankle flexibility and knee tracking, not strength yet."
                }
              ]
            },
            {
              "block_id": "D",
              "block_name": "D Block — Lower Back Rehab Core Circuit",
              "duration_minutes": 8,
              "exercises": [
                {
                  "exercise_id": "D1",
                  "name": "Dead Bug (anti-extension)",
                  "sets": 3,
                  "reps": "8 each side",
                  "rpe": "5",
                  "load_prescription": "BW",
                  "rest_seconds": 20,
                  "coaching_cue": "Lower back PINNED to mat. This is the anti-extension core exercise. Most important exercise for lower back health — teaches the core to resist extension forces that cause lower back pain."
                },
                {
                  "exercise_id": "D2",
                  "name": "Glute Bridge (loaded — DB on hips)",
                  "sets": 3,
                  "reps": "12 with 2s hold",
                  "rpe": "6",
                  "load_prescription": "DB on hips",
                  "rest_seconds": 20,
                  "coaching_cue": "Strong glute squeeze at top. Posterior chain strengthening is direct lower back treatment. Progress DB weight weekly."
                },
                {
                  "exercise_id": "D3",
                  "name": "Back Extension (bodyweight only — NO added load)",
                  "sets": 3,
                  "reps": "10 with 2s hold",
                  "rpe": "5",
                  "load_prescription": "BW ONLY — lower back injury means NO weighted back extension in Phase 1",
                  "rest_seconds": 20,
                  "coaching_cue": "IMPORTANT: BW only for this profile. Neutral spine at top — not hyperextension. This is controlled spinal extensor training, NOT heavy loading. Progress to light load in Phase 2 if pain-free."
                },
                {
                  "exercise_id": "D4",
                  "name": "Isometric Neck — 4-Way Series",
                  "sets": 1,
                  "reps": "10s × 4 directions",
                  "rpe": "4",
                  "load_prescription": "Manual resistance (hand on head)",
                  "rest_seconds": 10,
                  "coaching_cue": "Non-negotiable neck strengthening. Same as all other sessions."
                }
              ]
            },
            {
              "block_id": "E",
              "block_name": "E Block — Session A: Biceps + Shoulders (home gym version)",
              "duration_minutes": 5,
              "exercises": [
                { "exercise_id": "E1", "name": "DB Hammer Curl", "sets": 2, "reps": "12-15", "rpe": "6", "load_prescription": "Light DBs", "rest_seconds": 45, "coaching_cue": "Neutral grip. Full ROM — top to full extension. Slow eccentric." },
                { "exercise_id": "E2", "name": "Band Lateral Raise", "sets": 2, "reps": "15", "rpe": "6", "load_prescription": "Light band", "rest_seconds": 45, "coaching_cue": "Band under both feet. Raise to 90°. Control the descent." }
              ]
            },
            {
              "block_id": "F",
              "block_name": "F Block — Session A: Calf Raise (abbreviated — 45min constraint)",
              "duration_minutes": 3,
              "exercises": [
                { "exercise_id": "F1", "name": "Single-Leg Calf Raise", "sets": 2, "reps": "12-15 each leg", "tempo": "2-1-4-0", "rpe": "5", "load_prescription": "BW on step edge", "rest_seconds": 30, "coaching_cue": "45-min session: F Block to 1 exercise only. Slow eccentric calf raise. Full ROM." }
              ]
            }
          ]
        },

        {
          "session_id": "B",
          "notes": "Same structure as Session A. A Block: Cossack Squat (BW only) + Band Horizontal Row. B Block: Nordic isometric hold + DB Floor Press + Band Woodchop. E Block: Tricep variation + Rear Delt. F Block: Dead Hang 2×20s."
        },

        {
          "session_id": "C",
          "notes": "Posterior chain session with LOWER BACK MODIFICATIONS. A Block: SL Glute Bridge progression + DB Row (not bilateral deadlift). B1: Nordic isometric. B2: SL RDL (light DB, emphasis on glute not lower back). D3: Back Extension BW only. NOTE: Heavy bilateral hinging is CONTRAINDICATED for this profile."
        }
      ]
    },

    {
      "phase_number": 2,
      "phase_name": "Accumulation",
      "weeks": { "start": 5, "end": 8, "deload_week": 8 },
      "key_progressions": [
        "Nordic: isometric hold → start introducing partial eccentric lowering (3s down, catch at 45°)",
        "Back extension: introduce light DB if pain-free across Phase 1",
        "Split squat: increase DB load to Phase 2 moderate range",
        "McGill Big 3 still in every warm-up — never drop for this injury profile"
      ]
    },

    {
      "phase_number": 3,
      "phase_name": "Realization",
      "weeks": { "start": 9, "end": 12, "deload_week": 12 },
      "key_progressions": [
        "Nordic: progress to full eccentric if pain-free. 3-4 reps full range.",
        "SL RDL: increase load to moderate. Still no bilateral heavy deadlift.",
        "Back extension: light load only — prioritise quality not quantity",
        "Contrast pairs: Bulgarian SS → Box Step-Up (not jump — knee consideration)"
      ]
    }
  ],

  "deload_protocol": {
    "volume_reduction_percent": 45,
    "intensity_percent_of_peak": 65,
    "rpe_cap": 5,
    "blocks_to_reduce": ["A", "B", "E"],
    "blocks_to_maintain": ["C", "D", "warm_up"],
    "notes": "IMPORTANT for lower back injury: Do NOT skip warm-up or McGill Big 3 during deload weeks. Deload is still active training — it is not rest. Core and prehab volume maintained."
  },

  "readiness_assessment": {
    "factors": [
      { "name": "Sleep quality", "scale_min": 1, "scale_max": 10 },
      { "name": "Energy level", "scale_min": 1, "scale_max": 10 },
      { "name": "Motivation", "scale_min": 1, "scale_max": 10 },
      { "name": "Muscle soreness", "scale_min": 1, "scale_max": 10 },
      { "name": "Lower back pain (1=no pain, 10=severe)", "scale_min": 1, "scale_max": 10 }
    ],
    "thresholds": {
      "train_as_planned": "Average ≥ 6 AND lower back pain score < 4",
      "reduce_rpe_1": "Average 4-5.9 — reduce all RPE targets by 1 point",
      "reduce_rpe_2": "Lower back pain ≥ 4 — skip bilateral hinging, go bodyweight only",
      "active_recovery_only": "Lower back pain ≥ 7 — mobility and walking only, no loading"
    }
  }
}
```
