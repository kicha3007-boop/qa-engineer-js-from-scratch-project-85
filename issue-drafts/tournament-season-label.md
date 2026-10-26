# Bug: Tournament page names the season "the 4 2026 season"

Repository: https://github.com/hexlet-codebattle/codebattle (template "Bug Report", label `bug`)

### Summary

On a season tournament page the line about season points shows the season number and the year side by side ("the 4 2026 season"), while the season pages call it "Season 4, 2026".

Current version: frontend build `bea05b21db2ee2a63311d6f9fc2faca8` (the `version` field of the page's `data-page`), latest master commit at the time of testing: 285744f (2026-10-23).

### Reproduction steps

```bash
1. Open https://codebattle.hexlet.io/tournaments/5323 (tournament "Rookie", not signed in, interface language English)
2. Read the line under the tournament description
```

### Expected result

"Counts toward Season 4, 2026: the winner takes 8 season points."

### Actual result

"Counts toward the 4 2026 season: the winner takes 8 season points."

Screenshot: attach `assets/tournament-season-label-en.png` from https://github.com/kicha3007-boop/qa-engineer-js-from-scratch-project-85

### Browsers

Chrome (156.0.8078.47)

### OS

Windows (Windows 11 Pro 10.0.22000)
