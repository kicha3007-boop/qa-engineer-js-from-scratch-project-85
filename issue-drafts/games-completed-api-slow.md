# Bug: GET /api/v1/games/completed without filters takes 4.5–22.7 seconds

Repository: https://github.com/hexlet-codebattle/codebattle (template "Bug Report", label `bug`)

### Summary

The completed games endpoint without query parameters (20 latest games, ~8 KB) responds in several seconds, sometimes over 20 seconds. With a `user_id` filter (as the profile history tab calls it) it is much faster.

Current version: frontend build `bea05b21db2ee2a63311d6f9fc2faca8`, latest master commit at the time of testing: 285744f (2026-10-23).

### Reproduction steps

```bash
1. Send GET https://codebattle.hexlet.io/api/v1/games/completed
2. Repeat 5 times, one request at a time, 3 s pause between requests, and measure the response time
3. Compare with GET https://codebattle.hexlet.io/api/v1/games/completed?user_id=14968&page_size=20&page=1
```

### Expected result

The response arrives in under 3 seconds, like other public endpoints (/api/v1/tasks — 0.7 s, /api/v1/leaderboard/elo — 1.4 s).

### Actual result

All responses are 200, but take 5.83 s, 4.54 s, 4.59 s, 22.67 s and 6.80 s (2026-10-26, ~19:14 UTC). The same request with `?user_id=14968&page_size=20&page=1` takes 0.3–3.0 s.

Log: attach `assets/games-completed-api-timing.txt` from https://github.com/kicha3007-boop/qa-engineer-js-from-scratch-project-85

### Browsers

Not browser-specific (measured with Node.js 22.19.0 fetch)

### OS

Windows (Windows 11 Pro 10.0.22000)
