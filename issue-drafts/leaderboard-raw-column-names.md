# Bug: Season leaderboard column headers show raw field names (user_name, total_points, total_wins_count)

Repository: https://github.com/hexlet-codebattle/codebattle (template "Bug Report", label `bug`)

### Summary

The "Current Season Leaderboard" table on the Hall of Fame page (and the "Full Leaderboard" table on a season page) uses internal field names as column headers instead of human-readable labels.

Current version: frontend build `bea05b21db2ee2a63311d6f9fc2faca8` (the `version` field of the page's `data-page`), latest master commit at the time of testing: 285744f (2026-10-23). The UI no longer shows "Current version" in the footer.

### Reproduction steps

```bash
1. Open https://codebattle.hexlet.io/hall_of_fame (not signed in, interface language English)
2. Look at the column headers of the "Current Season Leaderboard" table
3. Open https://codebattle.hexlet.io/seasons/5 and look at the "Full Leaderboard" table
```

### Expected result

Readable headers, e.g. "Place", "Player", "Clan", "Points", "Wins", "Games", "Score", "Tournaments", "Avg place", "Best place", "Time".

### Actual result

Headers are raw field names: `place`, `user_name`, `clan_name`, `total_points`, `total_wins_count`, `total_games_count`, `total_score`, `tournaments_count`, `avg_place`, `best_place`, `total_time`.

Screenshot: attach `assets/hall-of-fame-columns-en.png` from https://github.com/kicha3007-boop/qa-engineer-js-from-scratch-project-85

### Browsers

Chrome (156.0.8078.47)

### OS

Windows (Windows 11 Pro 10.0.22000)
