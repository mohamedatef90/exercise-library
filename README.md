# Exercise Library

A dataset of 1,112 exercises with animated GIF demonstrations, muscle-targeting data, equipment, and step-by-step instructions, for use in fitness apps, websites, and scripts.

## Contents

```
exercises.json   Exercise database (about 1.4 MB, a JSON array of 1,112 entries)
gifs/            1,112 animated GIFs, one per exercise (about 100 MB)
```

Every entry points to an existing file in `gifs/`, and every `id` is unique.

## Data structure

```json
{
  "id": "2gPfomN",
  "name": "3/4 sit-up",
  "gif": "2gPfomN.gif",
  "targetMuscles": ["abs"],
  "secondaryMuscles": ["hip flexors", "lower back"],
  "bodyParts": ["waist"],
  "equipment": ["body weight"],
  "instructions": [
    "Step:1 Lie flat on your back with your knees bent and feet flat on the ground.",
    "Step:2 Place your hands behind your head with your elbows pointing outwards."
  ]
}
```

| Field | Type | Description |
| --- | --- | --- |
| `id` | string | Unique identifier |
| `name` | string | Exercise name |
| `gif` | string | File name of the GIF in `gifs/` |
| `targetMuscles` | array | Primary muscle (one value per exercise in the current data) |
| `secondaryMuscles` | array | Supporting muscles |
| `bodyParts` | array | Body region |
| `equipment` | array | Required equipment (one value per exercise in the current data) |
| `instructions` | array | Steps, each prefixed `Step:N` (4 to 11 steps per exercise) |

### Values in the data

- **`targetMuscles` (19 values):** abductors, abs, adductors, biceps, calves, cardiovascular system, delts, forearms, glutes, hamstrings, lats, levator scapulae, pectorals, quads, serratus anterior, spine, traps, triceps, upper back.
- **`bodyParts` (10 values):** back, cardio, chest, lower arms, lower legs, neck, shoulders, upper arms, upper legs, waist.
- **`equipment` (26 values):** assisted, band, barbell, body weight, bosu ball, cable, dumbbell, elliptical machine, ez barbell, hammer, leverage machine, medicine ball, olympic barbell, resistance band, roller, rope, skierg machine, sled machine, smith machine, stability ball, stationary bike, stepmill machine, tire, trap bar, weighted, wheel roller.
- **`secondaryMuscles` (36 values):** a different, larger vocabulary than `targetMuscles` (for example "abdominals", "quadriceps", and "deltoids" where `targetMuscles` uses "abs", "quads", and "delts"), so filter on it with care.

## Usage

```bash
git clone https://github.com/mohamedatef90/exercise-library.git
cd exercise-library
```

JavaScript:

```javascript
const exercises = require('./exercises.json');

const chest = exercises.filter(ex => ex.bodyParts.includes('chest'));
const pectorals = exercises.filter(ex => ex.targetMuscles.includes('pectorals'));
const bodyweight = exercises.filter(ex => ex.equipment.includes('body weight'));
const pushups = exercises.filter(ex => ex.name.toLowerCase().includes('push'));
```

Python:

```python
import json

with open('exercises.json', encoding='utf-8') as f:
    exercises = json.load(f)

bodyweight_only = [ex for ex in exercises if ex['equipment'] == ['body weight']]
print(len(bodyweight_only))
```

GIF URL pattern (served from this repository):

```javascript
const gifUrl = `https://raw.githubusercontent.com/mohamedatef90/exercise-library/main/gifs/${exercise.gif}`;
```

## Credits

- Exercise data: sourced from [ExerciseDB](https://rapidapi.com/justin-WFnsXH_t6/api/exercisedb).
- GIF demonstrations: community-contributed and curated.
- Maintained by [Mohamed Atef](https://github.com/mohamedatef90).
