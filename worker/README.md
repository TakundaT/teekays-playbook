# worker

Python service deployed on Railway.

- **Daily job**: pull the schedule, update team ratings from box scores, read the injury feed, write pre-game predictions to Supabase.
- **Live loop**: during games, poll `cdn.nba.com` play-by-play about every 10 seconds, compute win probability, write it to Supabase.

Uses only `cdn.nba.com` endpoints in production. Built in Phases 2 and 3.
