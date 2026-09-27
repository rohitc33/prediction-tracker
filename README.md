# Prediction Tracker

A single-file, fully local web app for tracking how accurate your predictions are.
Open `index.html` in any browser (phone or desktop). No server, no build step, and no network requests. All data lives in your browser's `localStorage`.

## Features
- Categories, each with its own predictions
- Each prediction has a stated probability (1–99%), an optional resolve-by date and notes
- Resolve a prediction with one tap (Happened / Didn't), or mark it Void to leave it out of scoring
- Per-category and overall stats: **accuracy**, **average specificity**, **bias**, Brier score
- Trend charts (all-time running average or rolling last 10) and a calibration breakdown
- Export and import a JSON backup (Menu → Export) to move data between devices

## Metrics
- **Specificity**: how far from a coin flip you are, `|p − 50| × 2`. 50% → 0%, 90% or 10% → 80%.
- **Accuracy**: share of resolved, non-50% predictions that went the way you leaned.
- **Bias**: average confidence in the side you picked, minus how often that side was right.
  Positive means overconfident; negative means underconfident.
- **Brier score**: mean of `(p − outcome)²`. Lower is better; always saying 50% gets 0.25.

## Install on your phone
Host the file anywhere static (for example, GitHub Pages) or open it locally, then use
"Add to Home Screen". Data is stored per browser and per origin, so export a backup before switching.
