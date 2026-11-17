# Architecture decisions

- **Logos**: official NBA team logos, used only to identify teams. Non-commercial site.
- **Production data**: `cdn.nba.com` only. `stats.nba.com` is used locally for history because it blocks cloud IPs.
- **Pre-game probability**: our own model. No sportsbook odds.
- **Sentiment analysis**: dropped for now. Injury and availability status is used instead.
- **Blog publishing**: TinaCMS. Posts are MDX files in this repo, written at `/admin`; Vercel redeploys on each commit.
- **Availability feature**: from who actually played in historical box scores for training, and from the day's injury report in production.
- **Cost**: about $5 USD/month (Railway worker), paused in the offseason; everything else on free tiers.

See the root README for the diagram and build phases.
