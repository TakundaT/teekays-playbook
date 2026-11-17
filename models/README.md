# models

Offline work, run on a local machine.

- `pull/`: scripts to download history from `stats.nba.com`: game logs (team + player rows, 2020-21 to 2025-26) for the pre-game model, play-by-play for the in-game model
- `notebooks/`: feature building, training, and evaluation (Brier score, calibration)
- `artifacts/`: exported model files loaded by the worker

Raw data lives in `models/data/` and is not committed. Built in Phase 0.
