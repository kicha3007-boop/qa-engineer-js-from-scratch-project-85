# Bug: Hall of Fame leaderboard column headers are still not translated into Russian (closed #2337)

Repository: https://github.com/hexlet-codebattle/codebattle (template "Bug Report", label `bug`)

### Summary

Closed issue: https://github.com/hexlet-codebattle/codebattle/issues/2337 (closed as completed on 2026-08-02). Step 5 of that report was "Go to the Hall of Fame and check the column headers". With the Russian interface the rest of the Hall of Fame page is translated, but the leaderboard column headers are still English (now they are even raw field names).

Current version: frontend build `bea05b21db2ee2a63311d6f9fc2faca8` (the `version` field of the page's `data-page`), latest master commit at the time of testing: 285744f (2026-10-23).

### Reproduction steps

```bash
1. Open https://codebattle.hexlet.io/ (not signed in)
2. Click the language button "EN" in the header and choose "Русский"
3. Open https://codebattle.hexlet.io/hall_of_fame
4. Look at the column headers of the "Таблица лидеров текущего сезона" table
```

### Expected result

Column headers are in Russian, e.g. "Место", "Игрок", "Клан", "Очки", "Победы", "Игры".

### Actual result

The table title, the search field ("Поиск по имени..."), the filters ("Все кланы", "Все языки") and the rest of the page are in Russian, but the column headers are `place`, `user_name`, `clan_name`, `total_points`, `total_wins_count`, `total_games_count`, `total_score`, `tournaments_count`, `avg_place`, `best_place`, `total_time`.

Screenshot: attach `assets/hall-of-fame-columns-ru.png` from https://github.com/kicha3007-boop/qa-engineer-js-from-scratch-project-85

### Browsers

Chrome (156.0.8078.47)

### OS

Windows (Windows 11 Pro 10.0.22000)
