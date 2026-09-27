# Prediction Tracker

A single-file, fully local web app for tracking how accurate your predictions are.
Open `index.html` in any browser (phone or desktop). No server, no build step, and no network requests. All data lives in your browser's `localStorage`.

## Features
- App-style layout with a bottom tab bar: **Home** (overall skill, predictions due to resolve, categories),
  **Predictions** (filter by category and open/resolved), **+** (new prediction), **Scores** (per-category
  scores and trends), **More** (manage categories, backup, erase)
- Categories, each with its own predictions
- Each prediction has a stated probability (1–99%), an optional resolve-by date and notes
- Resolve a prediction with one tap (Happened / Didn't), or mark it Void to leave it out of scoring
- Per-category and overall scores with 90% bootstrap ranges, plus trend charts and a calibration breakdown
- Predictions lock 15 minutes after entry, so the record can't be revised with hindsight
- Export and import a JSON backup (More → Export) to move data between devices

## Metrics
Each prediction has a probability `f` and, once resolved, an outcome `o` (1 = happened, 0 = didn't).
Scores use the Murphy decomposition of the Brier score:

```
Brier = mean((f − o)²)  ≈  Reliability − Resolution + Uncertainty
```

- **Skill score**: `1 − Brier / Uncertainty`, where `Uncertainty = ō(1 − ō)` and `ō` is how often things
  happened. This is the improvement over always guessing the base rate, so it's comparable across categories.
- **Calibration error**: `√Reliability`, in points. It's the typical gap between your stated probability and
  how often those things happened, with forecasts grouped into tenths (neighbouring groups are merged until
  each has at least 5). The tile also shows whether you lean overconfident or underconfident.
- **Resolution**: `Resolution / Uncertainty`, 0–100%. It measures how well your probabilities separate
  what happens from what doesn't.
- **Direction bias**: `mean(f) − ō`, in points. Positive means things happen less often than you predict.
- **Hit rate**: the share of predictions that went the way you leaned. Shown for reference only.

Scores appear after 5 resolved predictions and are greyed out below 20. Each score has a 90% bootstrap range.

## Locking
A prediction's statement, probability and "made on" date can be edited for 15 minutes after entry, then they
lock. Outcome, category, resolve-by date and notes stay editable. Predictions whose "made on" date is earlier
than the day they were entered show a "logged …" note.

## Install on your phone
Host the file anywhere static (for example, GitHub Pages) or open it locally, then use
"Add to Home Screen". Data is stored per browser and per origin, so export a backup before switching.
