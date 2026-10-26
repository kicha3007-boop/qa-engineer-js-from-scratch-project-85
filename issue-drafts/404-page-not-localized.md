# Bug: 404 page is shown in English when the Russian interface language is selected

Repository: https://github.com/hexlet-codebattle/codebattle (template "Bug Report", label `bug`)

### Summary

After switching the interface language to Russian, all regular pages are translated, but the 404 page stays in English and has `lang="en"`.

Current version: frontend build `bea05b21db2ee2a63311d6f9fc2faca8` (the `version` field of the page's `data-page`), latest master commit at the time of testing: 285744f (2026-10-23).

### Reproduction steps

```bash
1. Open https://codebattle.hexlet.io/ (not signed in)
2. Click the language button "EN" in the header and choose "Русский"
3. Open https://codebattle.hexlet.io/nonexistent-page
```

### Expected result

The 404 page is in Russian, e.g. "Страница не найдена" and a "На главную" button.

### Actual result

HTTP 404 with the text "404", "Page not found" and a "Home" button; `<html lang="en">`, while other pages show `lang="ru"` after the switch.

Screenshot: attach `assets/404-page-ru-locale.png` from https://github.com/kicha3007-boop/qa-engineer-js-from-scratch-project-85

### Browsers

Chrome (156.0.8078.47)

### OS

Windows (Windows 11 Pro 10.0.22000)
