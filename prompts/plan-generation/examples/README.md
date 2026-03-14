# Plan Generation — Few-Shot Examples

These examples are injected into the plan generation prompt at runtime as few-shot demonstrations. They show the model:

1. How to translate a quiz profile into a correctly structured plan
2. Correct block taxonomy (A-F), exercise selection, and pull:push ratio
3. Isometric and end-range progression across phases
4. Injury-specific exercise substitutions
5. F-block distribution rule

## Usage (in generate-plan Edge Function)

Inject examples into the human message BEFORE the user's quiz profile:

```
### Reference Examples

The following are example inputs and their correct plan outputs. Use these as format and decision-making guidance.

[example-01-commercial-gym-intermediate content]
[example-02-home-gym-lower-back content]

### Now generate a plan for this user:
[user quiz profile]
```

## Files

| File | Profile Type | Key Teaching Points |
|------|-------------|---------------------|
| `example-01-commercial-gym-intermediate.md` | Intermediate, commercial gym, no injury | Baseline session structure, all 6 blocks |
| `example-02-home-gym-beginner-lower-back.md` | Beginner, home gym, lower back sensitivity | Equipment substitutions, injury adaptations |
| `example-03-advanced-shoulder-impingement.md` | Advanced, anterior shoulder impingement | Complex injury protocol, pull-dominant pressing |
