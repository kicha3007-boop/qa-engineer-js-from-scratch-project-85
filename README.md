# Тестирование в продакшене: Codebattle

[![hexlet-check](https://github.com/kicha3007-boop/qa-engineer-js-from-scratch-project-85/actions/workflows/hexlet-check.yml/badge.svg)](https://github.com/kicha3007-boop/qa-engineer-js-from-scratch-project-85/actions)

Ручное тестирование работающего сервиса [Codebattle](https://codebattle.hexlet.io/): требования, тест-кейсы,
отчёт о прогоне, баг-репорты со скриншотами и логами, проверка закрытых баг-репортов (регресс).

Учебный проект Хекслета: https://ru.hexlet.io/programs/qa-engineer-js-from-scratch

## О Codebattle

[Codebattle](https://codebattle.hexlet.io/) — игра для программистов с открытым исходным кодом
([hexlet-codebattle/codebattle](https://github.com/hexlet-codebattle/codebattle)), которую развивает сообщество Хекслета.
Два игрока одновременно решают одну задачу, каждый на своём языке (17 языков), и видят код друг друга;
побеждает тот, чьё решение первым пройдёт все тесты. Можно играть с ботом (в том числе гостем, без регистрации),
с другом по ссылке и в турнирах. Другие пользователи могут наблюдать за игрой, завершённая игра доступна в записи.
Рейтинг строится по сезонам: игроки получают очки в турнирах сезона, лидеры попадают в «Зал славы».
Интерфейс и условия задач переводятся на русский, английский, испанский и китайский.

## Окружение и ограничения

- Google Chrome 156.0.8078.47 и Microsoft Edge 156.0.4314.42, Windows 11 Pro 10.0.22000; окно 1366x900,
  эмуляция экранов 375x812 и 393x852. Дата прогона — 26.10.2026.
- Версия Codebattle: строки «Current version: …» в подвале больше нет (закрытый issue #2186 — «так задумано»),
  поэтому в баг-репортах указана версия сборки фронтенда `bea05b21db2ee2a63311d6f9fc2faca8`
  (поле `version` в атрибуте `data-page` любой страницы) и последний коммит master на момент проверки — `285744f` (23.10.2026).
- Тестирование шло **без входа в аккаунт**: проверено всё, что доступно гостю (главная, тренировочная игра с ботом,
  наблюдение за игрой, записи игр, «Зал славы», сезоны, страницы турниров, вход и регистрация без отправки данных,
  переключение языков, тема, мобильная ширина, консоль и сеть DevTools). Лобби, профили, список задач, чат,
  игры с людьми и участие в турнирах требуют входа и в кейсы не вошли.
- Рейтинга «за неделю / месяц / всё время» из описания проекта больше нет: по ответу разработчиков в закрытом
  issue #2251 рейтинг заменён сезонными очками, поэтому требования сформулированы для сезонного рейтинга.
- Кейс «1000 одновременных пользователей» оформлен, но **не прогонялся**: нагрузочный тест чужого продакшена
  без согласования владельцев недопустим. Выполнение требования не подтверждено, поэтому в отчёте у кейса `fail`
  с пояснением, баг-репорта на него нет.

## Итоги

- Требований: 42 (26 функциональных, 9 нефункциональных, 7 неявных); на каждое — один тест-кейс.
- Тест-кейсов: 42; pass — 35, fail — 7 (6 баг-репортов + непрогнанный нагрузочный кейс).
- Найденные баги:
  1. Заголовки столбцов таблицы лидеров сезона — служебные имена полей (`user_name`, `total_points`, …).
  2. При русском интерфейсе эти заголовки не переведены (не исправленный пункт закрытого #2337).
  3. Страница 404 не переведена при русском интерфейсе.
  4. На странице турнира сезон назван «the 4 2026 season».
  5. Тесты задачи `nrzi_encoding` содержат не-ASCII символ «¯» — верное посимвольное решение на C++ проходит 3 теста из 30
     (уже описано в открытом [battle_asserts#1093](https://github.com/hexlet-codebattle/battle_asserts/issues/1093)).
  6. Публичный API `/api/v1/games/completed` без фильтров отвечает 4,5–22,7 с.

## Регресс: проверенные закрытые issue

Взяты issue, закрытые как выполненные (`state_reason: completed`), которые можно проверить без входа:

| Issue | Что проверено | Результат |
|---|---|---|
| [#2337](https://github.com/hexlet-codebattle/codebattle/issues/2337) | заголовки столбцов «Зала славы» на русском (шаг 5) | **не исправлено** — заголовки английские (`user_name`, `total_points`, …) |
| [#2351](https://github.com/hexlet-codebattle/codebattle/issues/2351) | второй гость по ссылке на чужую тренировочную игру не может править код | исправлено: «Cannot edit in read-only editor» |
| [#2362](https://github.com/hexlet-codebattle/codebattle/issues/2362) | на 393px панель навигации по тестам не перекрывает выбранный тест | исправлено |
| [#2332](https://github.com/hexlet-codebattle/codebattle/issues/2332), [#2231](https://github.com/hexlet-codebattle/codebattle/issues/2231) | «Sign up» после игры гостя ведёт на регистрацию, а не на 404 / GitHub | исправлено: открывается /users/new |
| [#2334](https://github.com/hexlet-codebattle/codebattle/issues/2334) | показ введённого пароля на страницах входа и регистрации | исправлено |
| [#1611](https://github.com/hexlet-codebattle/codebattle/issues/1611) | реванш гостя после тренировочной игры без ошибки 404 | исправлено: «Rematch» открывает новую игру |

Неисправленный #2337 указан в `reopened_issues.yml`; открытого дубликата нет.

Попутно: открытый [battle_asserts#1073](https://github.com/hexlet-codebattle/battle_asserts/issues/1073)
(неверные тесты `subnet_checker`) на проде уже не воспроизводится — все 27 тестов задачи совпадают с правильным
расчётом подсети. В `issues.yml` он не включён.

## Файлы

| Файл | Содержимое |
|---|---|
| `requirements.yml` | требования: `functional`, `non-functional`, `implicit` |
| `test-cases.yml` | тест-кейсы: summary, requirement, prerequisites, test-data, steps, expected-result |
| `testing-report.yml` | статус каждого кейса (`pass` / `fail`) |
| `bugreports.yml` | баг-репорты на упавшие кейсы: окружение, шаги, ожидаемый и фактический результат |
| `issues.yml` | ссылки на открытые issue в репозиториях hexlet-codebattle, которые описывают найденные баги |
| `reopened_issues.yml` | закрытые как выполненные issue, баг из которых не исправлен |
| `assets/` | скриншоты (`.png`) и логи (`.txt`), на которые ссылаются баг-репорты |

## Как повторить проверку самому

Нужны браузер (Chrome или Edge) и, для двух кейсов, Node.js 18+. Аккаунт на Codebattle и Хекслет не нужны.

1. Откройте https://codebattle.hexlet.io/ в окне инкогнито (гость, язык интерфейса English).
2. Откройте DevTools (F12): **Console** — ошибки скриптов, **Network** — коды ответов и время загрузки
   (включите *Disable cache*), **Application → Cookies** — cookie `_codebattle_key`.
3. Проходите кейсы из `test-cases.yml`; каждый независим — перед ним выполните его `prerequisites`.
   Для кейсов с игрой нажмите «Play your first battle» → «Start practice battle»: откроется игра с ботом,
   решение вводится в левый редактор, запуск — «Run». Для наблюдателя откройте ссылку на игру во втором браузере
   или втором окне инкогнито.
4. Мобильные кейсы — в Device Toolbar (Ctrl+Shift+M) с размером 375x812 или 393x852.
5. Сверяйте результат с `expected-result` и статусом в `testing-report.yml`; доказательства упавших кейсов — в `assets/`.
6. Время ответа API (по одному запросу, это не нагрузочный тест):

   ```bash
   node -e "(async()=>{for(let i=0;i<5;i++){const t=Date.now();const r=await fetch('https://codebattle.hexlet.io/api/v1/games/completed');await r.text();console.log(r.status,(Date.now()-t)+' ms');await new Promise(s=>setTimeout(s,3000))}})()"
   ```

7. Тесты задачи `nrzi_encoding` с проверкой символов:

   ```bash
   node -e "fetch('https://codebattle.hexlet.io/api/v1/tasks/32').then(r=>r.json()).then(j=>{const t=j.task||j;const s=new Set(t.asserts.flatMap(a=>[...a.arguments[0]]));console.log([...s].map(c=>c+' U+'+c.codePointAt(0).toString(16)+' '+Buffer.byteLength(c)+' bytes'))})"
   ```

Проверить, что yml-файлы читаются и соответствуют схемам автопроверки Хекслета:

```bash
npx --yes js-yaml test-cases.yml > /dev/null && echo ok
docker run --rm -v "$PWD:/project/code" hexletprojects/qa_engineer_codebattle_project_ru:latest sh -c "npm install && npx vitest run"
```

---

<details>
<summary>Автоматические тесты Хекслета</summary>

Тесты запускаются на каждый коммит. За запуск отвечает файл `.github/workflows/hexlet-check.yml` — не удаляйте и не переименовывайте ни его, ни репозиторий.

</details>

## О Хекслете

[Хекслет](https://ru.hexlet.io/) — школа программирования: авторские программы обучения с практикой, поддержкой наставников и реальными проектами, которые остаются в резюме. Этот репозиторий — один из таких проектов.
