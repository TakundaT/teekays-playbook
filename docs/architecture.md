# Architecture decisions

## Site and infrastructure

- **Logos**: official NBA team logos, used only to identify teams. Non-commercial site.
- **Production data**: `cdn.nba.com` only. `stats.nba.com` is used locally for history because it blocks cloud IPs.
- **Pre-game probability**: our own model. No sportsbook odds.
- **Sentiment analysis**: dropped for now. Injury and availability status is used instead.
- **Blog publishing**: TinaCMS. Posts are MDX files in this repo, written at `/admin`; Vercel redeploys on each commit.
- **Cost**: about $5 USD/month (Railway worker), paused in the offseason; everything else on free tiers.

## Models

- **Order**: models are built first (Phase 0), then the site.
- **Pre-game data pull**: `LeagueGameLog` team and player rows only, two calls per season. Play-by-play is pulled separately, only for the in-game model.
- **Train/serve parity**: the point-in-time feature code used in training is the same code the production worker runs daily.
- **Team strength**: Elo, not net rating (stable early in the season, carryover handles the blend with last season).
- **Availability feature**: minutes-based. From who actually played in historical box scores for training, and from the day's injury report in production. Questionable = half available.
- **Rest**: separate home/away back-to-back flags plus a 3-in-4 flag. Resting stars count toward availability, not rest.
- **Scope**: regular season only.
- **Split**: 2020-21 and 2021-22 Elo warm-up, 2022-23 and 2023-24 train, 2024-25 validate, 2025-26 test once.
- **Evaluation**: Brier score (primary), log loss, calibration plot. Calibration is the top priority. Options are only chosen if they win clearly across bootstrap resamples.

Full reasoning for the pre-game model: [`pregame-model.md`](pregame-model.md). See the root README for the diagram and build phases.
