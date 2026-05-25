# Paced Prototype

A browser-previewable React prototype built in-browser with Babel, React 18 CDN, and Tailwind CDN. No build step required for the prototype stage.

---

## How to open this on Windows

### Option A — Double-click (works for most screens)

1. Open File Explorer
2. Navigate to the `paced-prototype` folder
3. Double-click `index.html`

**This works for:** Today screen, Schedule, Profile, phone mockup, all visual elements.

**This may not work for:** The exercise catalog may fail to load in some Chromium-based browsers when opened via `file://` depending on your browser's security settings. If the catalog opens but shows no exercises, use Option B.

---

### Option B — VS Code Live Server (recommended, always works)

1. Open the `paced-prototype` folder in VS Code (`File → Open Folder`)
2. Install the **Live Server** extension (search "Live Server" in Extensions, install by Ritwick Dey)
3. Right-click `index.html` in the file explorer panel
4. Select **"Open with Live Server"**
5. Browser opens automatically at `http://127.0.0.1:5500`

This is the recommended method. It avoids all `file://` protocol restrictions and matches how GitHub Pages serves the files.

---

### Option C — GitHub Pages (for sharing)

Once this is pushed to GitHub:

1. Go to your repo on GitHub
2. Settings → Pages
3. Source: `Deploy from a branch`
4. Branch: `main`, folder: `/ (root)`
5. Save — GitHub generates a URL like `https://yourusername.github.io/paced-prototype/`

The relative paths (`src/styles/paced.css`, `src/data/exerciseCatalog.js`) work correctly on GitHub Pages.

---

## Folder structure

```
paced-prototype/
├── index.html                  ← Main entry point. Open this.
├── README.md                   ← This file.
└── src/
    ├── styles/
    │   └── paced.css           ← All global styles, design tokens, animations.
    └── data/
        └── exerciseCatalog.js  ← 1,729-exercise catalog (prototype inline data).
                                   Future: this moves to Supabase.
```

---

## GitHub workflow for this project

### First commit (save current state before any refactor)

```bash
git init
git add .
git commit -m "extract-styles-and-catalog-data"
```

### Ongoing commit naming convention

| Step | Commit name |
|---|---|
| This step | `extract-styles-and-catalog-data` |
| Next: move demo workout data | `extract-starter-data` |
| Next: extract catalog logic | `extract-catalog-engine` |
| Next: extract components | `extract-ui-components` |
| Next: extract screens | `extract-screen-files` |
| Later: schedule screen visuals | `add-schedule-visuals` |
| Later: profile screen visuals | `add-profile-visuals` |
| Later: onboarding flow | `add-onboarding-flow` |
| Later: Supabase schema | `connect-supabase-schema` |
| Later: OpenAI edge function | `connect-openai-edge-function` |

---

## Test checklist after opening

Run through these every time after a refactor step:

### Visual / shell
- [ ] Phone mockup renders (black bezel, rounded corners)
- [ ] Dynamic Island pill visible at top
- [ ] Topographic wallpaper visible (subtle gray paper-cut shapes behind content)
- [ ] Paced · Prototype label visible above phone
- [ ] Oswald font loads (workout names use condensed uppercase font)

### Today tab
- [ ] Today tab is active on load
- [ ] Workout card shows (black border, workout name large in Oswald)
- [ ] Tap the card — it expands showing exercise list
- [ ] Exercise names and set counts visible in expanded view
- [ ] Tap exercise name in expanded view opens Full Details
- [ ] Duration and muscle group labels visible on card

### Full Details / Workout Builder
- [ ] Workout name shown large at top (Oswald, editable)
- [ ] Tap the name — it becomes an editable input
- [ ] Edit name, press Enter or tap away — name saves
- [ ] Go back to Today — renamed card shows the new name
- [ ] Exercise cards visible with set/rep info
- [ ] Tap `>>>` (chevron tips) on an exercise — Advanced Sheet slides up
- [ ] Swipe left on a set row — red Delete appears, text centered in red area
- [ ] Long press an exercise card — drag reorder activates
- [ ] Swipe left on an exercise card — red Delete appears
- [ ] Tap "Add Exercise" dashed button — Catalog screen opens

### Catalog
- [ ] Catalog opens full screen
- [ ] Topographic wallpaper visible in catalog header area
- [ ] Title shows in Oswald uppercase ("ADD EXERCISE" or "SWAP [name]")
- [ ] Back button top-left returns to Full Details
- [ ] Horizontal tab strip: Chest, Back, Legs, Shoulders, Arms, Core, Cardio
- [ ] Tap Legs tab — exercises load (not blank)
- [ ] Sub-filter strip appears: Quads, Hamstrings, Glutes, Abductors, Adductors, Calves, Tibialis, Olympic
- [ ] Tap Hamstrings sub-filter — exercises update
- [ ] Equipment strip below sub-filters: All, Barbell, Dumbbell, Cable, Machine, Bodyweight, Kettlebell, Band
- [ ] Tap Dumbbell — list narrows to dumbbell exercises
- [ ] Hamstrings + Dumbbell filter: Romanian Dumbbell Deadlift should appear
- [ ] Search "bench" — bench press variations appear
- [ ] Search "lats" — lat pulldowns at top, NOT flat bench
- [ ] Search "tricep pushdown" — Cable Triceps Pushdown appears
- [ ] Search "rdl" — Romanian Deadlift variations appear
- [ ] Search "machine" — machine exercises appear
- [ ] Tap an exercise — closes catalog, exercise added to workout

### Advanced Sheet
- [ ] Opens from `>>>` button on an exercise
- [ ] Shows "Technique" selector at top (single selector for whole exercise)
- [ ] Shows sets list below
- [ ] Swipe left on a set row — Delete appears centered in red
- [ ] Large black plus at bottom — tap it adds a set
- [ ] "Make Superset" button — catalog opens in single-pick mode
- [ ] "Make Circuit" button — catalog opens in multi-pick mode
- [ ] X button closes sheet

### Schedule tab
- [ ] Tab bar navigates to Schedule
- [ ] Week list renders
- [ ] Custom workout names from Full Details appear on Schedule rows

### Active Workout
- [ ] Accessible via Start Workout button
- [ ] Dark theme renders
- [ ] Exercise list shows
- [ ] Checkmarks work
- [ ] Timer ticks

### State persistence (within session)
- [ ] Rename a workout in Full Details
- [ ] Navigate to Today tab — card shows renamed name
- [ ] Navigate to Schedule tab — renamed name shows there too
- [ ] Add an exercise via catalog
- [ ] Go back to Today, expand card — new exercise appears in list

---

## What is prototype-only (do not architect around this)

- `PUSH`, `PULL`, `LEGS`, `CARDIO`, `WEEK` in `index.html` — demo split data only, not final app structure
- `customNames` / `customItems` state in App — prototype substitute for Supabase user_splits
- `STREAK = 12` — hardcoded demo number
- `"12,800 lbs"` in DaySheet — hardcoded placeholder
- All exercise data in `exerciseCatalog.js` — will migrate to Supabase `exercise_catalog` table

---

## What should NOT be in this file in the final app

| Currently in | Should become |
|---|---|
| `src/data/exerciseCatalog.js` | Supabase `exercise_catalog` table |
| `PUSH/PULL/LEGS/CARDIO` in index.html | Supabase `template_splits` table |
| `WEEK` in index.html | Supabase `calendar_workouts` table |
| `customNames` in App state | Supabase `user_splits.name` |
| `customItems` in App state | Supabase `user_workout_exercises` table |

---

## OpenAI API — important

Do not put any OpenAI API key in this file, any frontend file, or any browser-visible code.

The final AI integration path:
1. Frontend calls `suggestExerciseSwap(exerciseId, reason)` — a clean function call
2. That function calls a Supabase Edge Function
3. The Edge Function holds the secret API key in its environment variables
4. Edge Function calls OpenAI, validates the response, returns structured JSON
5. Frontend applies the structured JSON safely

This file should never contain `sk-...` or any API key.
