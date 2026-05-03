# Phase 1 Features — Testing Guide

All Phase 1 features have been implemented in commit `444cc08`. This guide walks through testing each feature.

## Setup Instructions

1. Open `index.html` in your browser (or run `npm start` / `python -m http.server 8000`)
2. For clean testing, open DevTools (F12) → Application → Local Storage → clear all keys
3. Reload the page

---

## Feature 1: Setup Modal Fixes

### Test: Auto-close on both selections
1. Clear localStorage and reload
2. Click any **theme** button (🌙 or ☀️)
3. Click any **accent color** button (blue/green/purple/orange)
4. Expected: Modal closes **immediately** after color selection (no countdown)

### Test: X button with Dark+Orange default
1. Clear localStorage and reload
2. Click only a **theme** (don't select color)
3. Click the **✕** button at top-right
4. Reload the page
5. Expected: 
   - Modal should NOT appear (already closed with defaults)
   - App should be Dark theme + Orange accent

### Test: Modal shows only once
1. After setting theme/color and closing modal, reload multiple times
2. Expected: Modal should never appear again

---

## Feature 2: Set Completion Tracking

### Test: Checkmark button and circles
1. Complete Feature 1 setup first
2. Click "Day 1" to start a workout
3. Enter weight and reps for **Set 1** (e.g., 185 lbs, 8 reps)
4. Click the **✓** button in the Reps column
5. Expected:
   - First circle (●) fills with accent color
   - Counter shows "1/3 Sets Complete"
   - Button background fills with accent color

### Test: Toggle completion
1. Click the ✓ button again
2. Expected:
   - Circle unfills (becomes ○)
   - Counter goes back to "0/3 Sets Complete"
   - Button background becomes transparent

### Test: Multiple sets
1. Enter weight/reps for Set 2 and Set 3
2. Click ✓ on Set 1, 2, and 3
3. Expected: Circles fill in order (●●●), counter shows "3/3 Sets Complete"

---

## Feature 3: Per-Set Previous Weight Display

### Test: First workout (no previous data)
1. Start Day 1 workout (Feature 2 above)
2. Look under each set's weight input
3. Expected: See "Previous: Not tracked" in small gray text

### Test: Second workout shows previous weights
1. **Complete the workout** (click "✓ Complete Workout" button)
2. Click "Day 1" again to start another workout
3. Look under weight inputs
4. Expected: See "Previous: 185 lbs" (or whatever you entered) for each set

### Test: Per-set granularity
1. On second workout, enter different weights for different sets:
   - Set 1: 190 lbs
   - Set 2: 185 lbs
   - Set 3: 180 lbs
2. Complete workout
3. Start Day 1 again
4. Expected: Each set shows its own previous weight, not a summary

---

## Feature 4: Warm-up / Cool-down Sections

### Warm-up Section

#### Test: Treadmill auto-save
1. Start any workout (Day 1, 2, or 3)
2. Scroll to **🏃 Warm-up (5-10 mins)** section
3. Change treadmill values:
   - Time: 15 mins
   - Speed: 6 kph
4. Click "Mark Done" button
5. Expected:
   - Button turns accent color (filled)
   - Text changes to "✓ Done"
6. Go back to home, start a NEW workout on the **same day**
7. Expected: Treadmill should default to 15 mins, 6 kph

#### Test: Day-specific stretches
1. Look at the stretches in warm-up for **Day 1**:
   - Expected: Chest Stretch, Shoulder Stretch, Tricep Stretch, Back Stretch
2. Cancel and start **Day 2**
3. Expected stretches: Quad Stretch, Hamstring Stretch, Hip Flexor Stretch, Calf Stretch
4. Cancel and start **Day 3**
5. Expected stretches: Lat Stretch, Shoulder Stretch, Upper Back Stretch, Neck Stretch

#### Test: Stretch completion
1. Click "Done" on any stretch
2. Expected:
   - Text becomes strikethrough and faded
   - Button changes to "✓" and fills with accent color
3. Click again to uncomplete
4. Expected: Strikethrough removed, button goes back to "Done"

### Cool-down Section

#### Test: Mirror of warm-up
1. Scroll down to **🧘 Cool-down (5-10 mins)** section
2. Verify it has:
   - Same day-specific stretches (same as warm-up)
   - Treadmill section (appears **after** stretches, reversed from warm-up)
3. Enter treadmill values and click "Done"
4. Expected: Values persist to `appState.workoutDefaults.cooldownTreadmill`

---

## Feature 4 Advanced: Verifying Data Persistence

### localStorage Inspection
1. Open DevTools (F12)
2. Go to **Application → Local Storage** → select this page
3. Look for `workoutTrackerState` key
4. Click to view full value
5. Expected JSON structure:
```json
{
  "theme": "dark",
  "accentColor": "orange",
  "showedInitialSetup": true,
  "isRestartMode": false,
  "restartWeek": 1,
  "workoutDefaults": {
    "warmupTreadmill": { "time": 15, "speed": 6 },
    "cooldownTreadmill": { "time": 10, "speed": 2.5 }
  }
}
```

### Session Persistence
1. Enter data in warm-up/cool-down sections but DO NOT complete workout
2. Close the tab
3. Reopen `index.html`
4. Click "Day 1" again
5. Expected: **Warm-up/cool-down state resets** (not persisted during incomplete session)
6. But treadmill **defaults** (from completed sessions) should be remembered

---

## Full Integration Test

**Scenario:** Complete a full workout from start to finish

1. **Setup Modal** → Select Dark theme + Green accent → Modal closes immediately
2. **Day 1 Workout**
   - Warm-up: 12 mins treadmill, 5 kph; mark stretches done
   - Chest Press: 185×8, 190×8, 185×8 (mark all sets complete)
   - All exercises: enter weights/reps, mark sets complete
   - Cool-down: 10 mins treadmill, 2.5 kph; mark stretches done
   - Click "✓ Complete Workout"
3. **Day 1 Again** (new session)
   - Warm-up: treadmill should default to 12 mins, 5 kph
   - Chest Press Set 1: should show "Previous: 185 lbs"
4. **Settings**: Open Settings modal (should show Dark + Green selected)

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Setup modal keeps appearing | Clear localStorage: DevTools → Application → Local Storage → Delete all |
| Previous weights show "Not tracked" | You need to complete a workout first; start a new day after |
| Treadmill defaults don't save | Make sure to click "Mark Done" button, not just fill in values |
| Circles don't fill on checkmark | Click the checkmark button (✓) in the Reps column, not elsewhere |
| App shows old version | Hard refresh: Ctrl+Shift+R (or Cmd+Shift+R on Mac) |

---

## Notes for Developers

- All state is in `appState` and persisted via `saveState()` to localStorage
- `currentSession` state does NOT persist mid-workout (by design)
- Setup modal only shows if `showedInitialSetup === false`
- Color circles use `flex-shrink: 0` to maintain perfect circular shape
- Stretch lists are defined in `STRETCHES` constant and populated via `getWarmupStretches(day)` / `getCooldownStretches(day)`
- All functions properly handle edge cases (null checks, default values, etc.)
