# Few-Shot Example 03 — Advanced Lifter, Anterior Shoulder Impingement

Demonstrates: complex injury protocol (shoulder), pressing substitutions,
pull-dominant A Block Session C, overhead press elimination with safe
alternatives, advanced load prescriptions.

---

## Input Profile (Key Fields)

```json
{
  "persona_id": "example-03",
  "age": 38,
  "biological_sex": "male",
  "training_experience": "advanced",
  "training_history": "10 years. Competitive powerlifting for 4 years. Now training for general strength + longevity.",
  "goals": { "primary": "strength", "secondary": "longevity", "tertiary": "muscle_gain" },
  "injuries": [
    {
      "location": "right_shoulder",
      "type": "anterior impingement — diagnosed by physio. Worse with overhead pressing and internal rotation under load.",
      "severity": "moderate",
      "contraindicated_movements": [
        "overhead_barbell_press",
        "upright_row",
        "behind_neck_press",
        "internal_rotation_loaded",
        "front_raise_heavy"
      ],
      "required_prehab": [
        "band_external_rotation",
        "face_pull",
        "wall_slide",
        "serratus_anterior_activation"
      ]
    }
  ],
  "equipment": {
    "location": "commercial_gym",
    "available": ["barbell", "dumbbells", "cables", "machines", "pull_up_bar", "rings", "landmine", "hex_bar", "bands"]
  },
  "schedule": {
    "days_per_week": 4,
    "session_duration_minutes": 75,
    "preferred_days": ["monday", "tuesday", "thursday", "friday"]
  }
}
```

---

## Critical Injury Decision Points

1. **Overhead press ELIMINATED** from Session C A Block → replaced with landmine press (neutral grip, shoulder-safe angle)
2. **Upright row NEVER programmed** → face pull and cable external rotation instead
3. **Session B A2 pressing** → Floor press or neutral-grip DB press (not barbell bench — internal rotation risk)
4. **Prehab mandatory in EVERY warm-up** → Band external rotation + face pull before any pressing
5. **Advanced load prescription** → RPE 8-9 from Week 1 (experienced athlete tolerance)
6. **Nordic at full eccentric + concentric from Phase 1** (advanced baseline)

---

## Expected Plan Output (Session C A Block + Full Shoulder Injury Notes)

> Full plan follows Example 01 structure. This example focuses on the key injury
> adaptations in Session C and pressing selections across all sessions.

```json
{
  "plan_metadata": {
    "plan_id": "example-03-plan",
    "methodology_version": "cressey-hybrid-v1",
    "duration_weeks": 12,
    "sessions_per_week": 4,
    "injury_flags": [
      {
        "location": "right_shoulder",
        "type": "anterior impingement",
        "severity": "moderate",
        "contraindicated_movements": [
          "overhead_barbell_press",
          "upright_row",
          "behind_neck_press",
          "internal_rotation_loaded",
          "front_raise_heavy"
        ],
        "required_prehab": [
          "band_external_rotation",
          "face_pull",
          "wall_slide",
          "serratus_anterior_activation"
        ]
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

  "shoulder_injury_modifications": {
    "pressing_rules": [
      "No barbell overhead press under any circumstances — anterior impingement contraindication.",
      "Landmine press is the primary overhead substitute: neutral grip, shoulder moves in pain-free arc.",
      "DB pressing preferred over barbell bench — allows natural wrist and shoulder rotation.",
      "Ring dip permitted ONLY if pain-free. If any impingement: floor press substitute.",
      "No internal rotation under load — includes any exercise that internally rotates humerus while loaded (upright row, heavy front raise)."
    ],
    "prehab_protocol": {
      "exercises_every_session": [
        { "name": "Band External Rotation (elbow at 90°)", "sets": 2, "reps": "15 each side", "notes": "Highest priority prehab. Shoulder health depends on external rotator strength." },
        { "name": "Face Pull with External Rotation", "sets": 2, "reps": "15", "notes": "Mandatory before any pressing. Prepares rotator cuff." },
        { "name": "Wall Slide", "sets": 1, "reps": "10", "notes": "Serratus anterior activation — prevents winging scapula which worsens impingement." }
      ]
    },
    "pressing_hierarchy": [
      "1st choice: Landmine Press (neutral grip, 30-45° from body)",
      "2nd choice: DB Floor Press (natural wrist rotation, limited ROM = safe)",
      "3rd choice: Ring Dip (self-selecting safe ROM — only if pain-free)",
      "Eliminated: Barbell OHP, Upright Row, Behind-Neck Press, Heavy Front Raise"
    ]
  },

  "phases": [
    {
      "phase_number": 1,
      "phase_name": "Foundation",
      "weeks": { "start": 1, "end": 4, "deload_week": 4 },
      "rep_range_primary": "6-8",
      "rpe_range": "7-8",
      "isometric_type": "yielding",

      "sessions": [
        {
          "session_id": "A",
          "session_type": "Sagittal — Bulgarian Split Squat + Weighted Pull-Up",
          "notes": "Session A: No pressing in A Block (vertical pull superset with split squat). Shoulder not stressed.",
          "blocks": [
            {
              "block_id": "warm_up",
              "block_name": "Warm-Up (Shoulder Prehab Priority)",
              "exercises": [
                { "exercise_id": "WU1", "name": "Band External Rotation (elbow at 90°)", "sets": 2, "reps": "15 each", "rpe": "4", "load_prescription": "Light band", "coaching_cue": "MANDATORY before any session. Elbow pinned to side, rotate outward. Slow return. This is rotator cuff strengthening." },
                { "exercise_id": "WU2", "name": "Face Pull with External Rotation", "sets": 2, "reps": "15", "rpe": "4", "load_prescription": "Light cable", "coaching_cue": "Pull to forehead, rotate wrists back at peak. Lower trap + external rotator activation." },
                { "exercise_id": "WU3", "name": "Wall Slide", "sets": 2, "reps": "10", "rpe": "4", "load_prescription": "BW", "coaching_cue": "Forearms flat on wall, slide up to overhead. Serratus anterior activation." },
                { "exercise_id": "WU4", "name": "World's Greatest Stretch", "sets": 1, "reps": "5 each", "rpe": "4", "load_prescription": "BW", "coaching_cue": "Full movement prep." },
                { "exercise_id": "WU5", "name": "Foam Roll T-Spine", "sets": 1, "reps": "60s", "rpe": "4", "load_prescription": "Foam roller", "coaching_cue": "Thoracic mobility. Poor T-spine mobility compensates at shoulder — direct treatment for impingement." }
              ]
            },
            {
              "block_id": "A",
              "block_name": "A Block — Bulgarian Split Squat + Weighted Pull-Up",
              "exercises": [
                { "exercise_id": "A1", "name": "Bulgarian Split Squat", "sets": 4, "reps": "6-8 each leg", "tempo": "3-1-2-0", "rpe": "8", "load_prescription": "Heavy DBs (challenging for advanced lifter)", "superset_with": "A2", "coaching_cue": "Advanced load from Week 1. Front shin vertical. Drive through full foot. 4 sets — advanced volume.", "movement_category": "squat" },
                { "exercise_id": "A2", "name": "Weighted Pull-Up", "sets": 4, "reps": "5-6", "tempo": "3-1-2-0", "rpe": "8", "load_prescription": "Weight belt + 10-20kg depending on baseline", "superset_with": "A1", "coaching_cue": "Full dead hang each rep. Pronated grip. SHOULDER NOTE: Pull-ups are safe for anterior impingement — the motion is humeral depression and retraction, not internal rotation.", "movement_category": "pull" }
              ]
            },
            {
              "block_id": "B",
              "block_name": "B Block — Nordic Full + DB Floor Press + Landmine Rotation",
              "exercises": [
                { "exercise_id": "B1", "name": "Nordic Curl (Full Eccentric + Concentric — Advanced)", "sets": 4, "reps": "5-6 full range", "tempo": "5-0-3-0", "rpe": "8", "load_prescription": "BW → add resistance vest in Phase 2", "coaching_cue": "Advanced baseline: full eccentric AND full concentric push back up. 5s lowering. This is the advanced standard.", "movement_category": "pull" },
                { "exercise_id": "B2", "name": "DB Floor Press (shoulder-safe pressing)", "sets": 4, "reps": "6-8", "tempo": "3-1-2-0", "rpe": "8", "load_prescription": "Heavy DBs", "coaching_cue": "SHOULDER SAFE CHOICE: Floor press limits ROM naturally — avoids the end-range position where impingement occurs. Heavy DB allows natural wrist rotation. DO NOT use barbell bench for this profile.", "movement_category": "push" },
                { "exercise_id": "B3", "name": "Landmine Rotation (anti-rotation progression)", "sets": 4, "reps": "8 each side", "tempo": "2-1-2-0", "rpe": "7", "load_prescription": "Moderate barbell in landmine", "coaching_cue": "Rotate through thoracic spine. The landmine allows a pain-free pressing arc — shoulder-safe rotational pressing variation.", "movement_category": "rotation" }
              ]
            }
          ]
        },

        {
          "session_id": "C",
          "session_type": "Posterior Chain — Hex Bar DL + LANDMINE PRESS (not barbell OHP)",
          "notes": "CRITICAL SESSION: This is where overhead press would normally appear (Session C A Block). SUBSTITUTED with Landmine Press due to anterior shoulder impingement.",
          "blocks": [
            { "block_id": "warm_up", "notes": "Same shoulder prehab warm-up every session. Band ER + Face Pull mandatory." },
            {
              "block_id": "A",
              "block_name": "A Block — Hex Bar Deadlift + Landmine Press (OHP substitute)",
              "exercises": [
                {
                  "exercise_id": "A1",
                  "name": "Hex Bar Deadlift",
                  "sets": 4,
                  "reps": "4-6",
                  "tempo": "3-1-2-0",
                  "rpe": "8",
                  "load_prescription": "Heavy — advanced athlete can deadlift significant weight",
                  "superset_with": "A2",
                  "coaching_cue": "Standard hex bar hip hinge. No shoulder involvement. Advanced load expected.",
                  "movement_category": "hinge"
                },
                {
                  "exercise_id": "A2",
                  "name": "Landmine Press (seated or standing — bilateral)",
                  "sets": 4,
                  "reps": "6-8",
                  "tempo": "3-1-2-0",
                  "rpe": "7-8",
                  "load_prescription": "Moderate — do NOT push to max load on shoulder injury",
                  "superset_with": "A1",
                  "coaching_cue": "INJURY SUBSTITUTION: Overhead barbell press is CONTRAINDICATED. Landmine press provides a 30-45° arc from body — safe for anterior impingement because: (1) neutral grip eliminates internal rotation, (2) the arc doesn't enter the painful overhead position. Grip the end of the barbell in landmine. Press forward and upward in a natural arc. No pain should be experienced. If pain occurs, drop to DB Floor Press.",
                  "movement_category": "push",
                  "substitutions": [
                    { "name": "DB Floor Press", "reason": "If landmine press causes any shoulder pain" },
                    { "name": "Ring Dip (pain-free range)", "reason": "If seeking more vertical press pattern and pain-free" }
                  ]
                }
              ]
            }
          ]
        }
      ]
    },

    {
      "phase_number": 2,
      "phase_name": "Accumulation",
      "weeks": { "start": 5, "end": 8, "deload_week": 8 },
      "shoulder_progressions": [
        "Landmine press: increase load if pain-free. Consider progressing to standing single-arm landmine press.",
        "Assess pain response — if shoulder improved, may trial light DB overhead press (pain-free range only) with physio sign-off.",
        "Nordic: add resistance vest (5-10kg). Still full eccentric + concentric.",
        "Face Pull: progress to cable external rotation with heavier cable."
      ]
    },

    {
      "phase_number": 3,
      "phase_name": "Realization",
      "weeks": { "start": 9, "end": 12, "deload_week": 12 },
      "shoulder_progressions": [
        "Landmine press contrast pair: heavy landmine 3-4 reps → explosive push-up (neutral wrist) 3-4 reps.",
        "If shoulder completely pain-free and cleared by physio: light barbell OHP (70% max, pain-free ROM). Otherwise maintain landmine.",
        "Nordic: loaded vest + faster eccentric intent.",
        "Band ER + Face Pull: maintain every single session — never drop prehab even in Phase 3."
      ]
    }
  ],

  "deload_protocol": {
    "volume_reduction_percent": 45,
    "intensity_percent_of_peak": 65,
    "rpe_cap": 6,
    "blocks_to_reduce": ["A", "B", "E"],
    "blocks_to_maintain": ["C", "D", "warm_up"],
    "notes": "SHOULDER INJURY: Shoulder prehab (band ER, face pull, wall slide) is ALWAYS maintained at full volume — even on deload weeks. Prehab is not optional."
  },

  "readiness_assessment": {
    "thresholds": {
      "train_as_planned": "Average ≥ 6 AND zero shoulder pain during prehab",
      "reduce_rpe_1": "Shoulder ache (1-2/10 pain) — reduce pressing load 20%, increase prehab sets",
      "reduce_rpe_2": "Shoulder pain 3-4/10 — eliminate ALL pressing. Pulls, legs, core only.",
      "active_recovery_only": "Shoulder pain ≥ 5/10 — mobility and walking only. Physio consult."
    }
  }
}
```

---

## Summary: Shoulder Impingement Substitution Reference

| Standard Exercise | Impingement Substitute | Reason |
|---|---|---|
| Barbell Overhead Press | Landmine Press (neutral grip) | Eliminates internal rotation arc |
| Upright Row | Face Pull + External Rotation | Reverses the impingement mechanism |
| Heavy Front Raise | Band External Rotation | Target external rotators instead |
| Behind-Neck Press | ELIMINATED — no substitute | Never program this variant |
| Ring Dip (if pain-free) | DB Floor Press | Floor press if any pain |

**Rule:** When in doubt, choose MORE pulling exercises. The pull:push ratio for this
profile should skew toward 4:2 or even 5:2 where possible to reduce anterior
shoulder load and reinforce external rotation strength.
