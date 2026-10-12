# Проверьте рекламную выгрузку вместе с ИИ-агентом

[Каталог](README.ru.md) · [Architecture](ARCHITECTURE.md) · [English instructions](#english-instructions)

Начните с выдуманного отчёта. Агент получит конкретный инструмент, а вы увидите, как проверить расчёт. Для примера нужны Python 3.9+ и файлы direct-report-audit v0.1.0. Доступ к рекламному кабинету не нужен.

Если хотите сравнить цены, сроки и состав двух предложений, перейдите к [установке competitor-offer-radar](#radar-current-source). Это другой самостоятельный модуль той же системы.

## Получить модуль

Скачайте ZIP на странице [release v0.1.0](https://github.com/ilookatshow-gif/direct-report-audit/releases/tag/v0.1.0), распакуйте в новый каталог и откройте его в Codex или Claude Code. Этот каталог Lookatshow содержит ссылки и инструкции, а не сам инструмент.

Если предпочитаете Git, из выбранного места, где ещё нет папки `direct-report-audit`:

```sh
git clone --branch v0.1.0 --single-branch https://github.com/ilookatshow-gif/direct-report-audit.git
cd direct-report-audit
```

Выполните из каталога модуля:

```sh
python3 -B direct_report_audit.py --json doctor
python3 -B direct_report_audit.py schema
python3 -B -m unittest discover -s tests -v
python3 -B direct_report_audit.py --json audit examples/synthetic-placements.csv --min-clicks 20 --min-cost 1000 --max-cpa 1000 --min-conversions 1
```

На Windows используйте `python` вместо `python3`, если так называется ваш Python. Наличие команды не заменяет проверку своей среды: doctor и tests запускаются у вас.

## Что должно получиться

08.10.2026 команды doctor и audit дали exit 0 на macOS arm64, Python 3.9.6; unit tests прошли 25/25. Исходник CLI и учебный CSV совпали по Git blob SHA с публичным тегом v0.1.0. Это проверка конкретного примера, не универсальный тест всех платформ.

Doctor возвращает `ok=true`, version `0.1.0`, `offline=true`, `auth_required=false`, `network=false`.

В JSON audit найдите:

| Поле | Значение учебного примера |
|---|---|
| `result.input.synthetic` | `true` |
| `result.input.rows` / `placements` | `5` / `4` |
| `result.totals.impressions` / `clicks` | `4550` / `97` |
| `result.totals.cost` / `conversions` | `"6000"` / `"5"` |
| `result.totals.cpc` / `cpa` | `"61.86"` / `"1200.00"` |
| `result.candidate_count` | `2` |

У `costly.example.invalid` CPA равен 2500, выше выбранного порога 1000; причина `cpa_above_threshold`. Две строки `example.invalid` суммируются: расход 1800, 30 кликов, 0 конверсий; причина `zero_conversion_spend`. У этой площадки CPA равен `null`, поскольку делить на ноль нельзя.

Все цифры и площадки выдуманы. Два кандидата означают «проверить», а не «отключить» и не «сэкономить 4300». Сначала нужно учесть период, цели, задержку атрибуции и качество лидов. Пороги в команде выбраны для примера, не как норматив рынка.

## Скажите агенту

Скопируйте в Codex или Claude Code после открытия каталога модуля:

> Прочитай README.ru.md и AGENTS.md direct-report-audit. Запусти doctor, schema, unit tests и audit на examples/synthetic-placements.csv с min-clicks=20, min-cost=1000, max-cpa=1000, min-conversions=1. Покажи суммы и двух кандидатов, объясни причины. Сверь результат с исходным CSV. Учебные данные не называй кейсом клиента. Пока ничего не устанавливай, не подключай кабинеты и не меняй рекламу. Не публикуй мои файлы.

Первый результат можно получить без установки. Если нужна постоянная локальная команда, используйте install.py по инструкции самого модуля, выбрав свой prefix. Авторский onboard запускается один раз с явно выбранным локальным state-файлом; обычный audit не выводит рекламное приветствие.

## Затем своя выгрузка

Нормализуйте её локально к пяти полям: `Placement,Impressions,Clicks,Cost,Conversions`. Удалите служебные строки и итоги. Не смешивайте валюты, периоды, цели или модели атрибуции; `Cost` задаётся в денежных единицах, не в микроденежных единицах API. Полный контракт находится в README модуля.

Для следующего запуска выберите собственные пороги и конкретный файл. При ошибке входа утилита не выдаёт частичные суммы. Кандидаты остаются предметом ручной проверки. Если облачный агент видит ваши данные, соблюдайте правила провайдера и своей компании.

## English instructions

Download and unpack [v0.1.0](https://github.com/ilookatshow-gif/direct-report-audit/releases/tag/v0.1.0), or clone the tag using the commands above. Open the module directory in your agent. Run doctor, schema, tests and the synthetic audit before supplying your own export. Python 3.9+ is required; use `python` on Windows if that's your command name.

Copyable prompt:

> Read direct-report-audit's README.md and AGENTS.md. Run doctor, schema, unit tests and audit on examples/synthetic-placements.csv with min-clicks=20, min-cost=1000, max-cpa=1000 and min-conversions=1. Explain the totals and two manual-review candidates; check them against the CSV. These are invented educational data, not a customer case. Don't install anything yet, connect accounts, change campaigns or publish my files.

Expected audit: five rows, four placements, 6000 RUB cost, 97 clicks, five conversions, CPC 61.86, CPA 1200.00 and two candidates. `synthetic=true`. A successful local calculation isn't a savings claim; review tracking, attribution and lead quality before decisions.

<a id="radar-current-source"></a>
## Сравнить предложения: дайте архив своему агенту

[Скачайте проверенный ZIP исходников](https://github.com/ilookatshow-gif/competitor-offer-radar/archive/7206178f1f6c7484c6f4463c62fe48d497b398d6.zip), распакуйте и откройте полученный каталог в Codex или Claude Code. Для работы нужен Python 3.9+, но кабинет, токены, подписка и покупка ядра не нужны.

Скопируйте запрос:

> Прочитай README.ru.md и AGENTS.md в этом архиве competitor-offer-radar. Установи инструмент в новый каталог снаружи исходников, не меняя системный PATH. Запусти doctor, тесты, validate для examples/before.json и examples/after.json, затем compare этих двух файлов. Покажи исходные суммы, сроки и изменение состава; объясни, почему изменённые пакеты нельзя сравнивать только по цене. Выполни onboard один раз с отдельным локальным state-каталогом. Никакие сайты не собирай, кабинеты не подключай, мои данные не публикуй. Если Python или нужные права отсутствуют, назови препятствие, не выдавай установку за завершённую.

Для проверки вручную, из распакованного каталога:

```sh
python3 -B competitor_offer_radar.py doctor
python3 -B competitor_offer_radar.py validate examples/before.json
python3 -B competitor_offer_radar.py validate examples/after.json
python3 -B competitor_offer_radar.py compare examples/before.json examples/after.json
python3 -B tests/smoke_install.py
```

На Windows используйте `python`, если ваш интерпретатор называется так. Проверка установки сама использует новый временный каталог и не меняет ваши рабочие файлы.

В учебном результате: сумма 10 000 → 12 500 RUB (+25%), срок 4 → 6 рабочих дней (+50%), интервью 2 → 1; `scope_changed_warning=true`. Это выдуманные данные, не доказательство качества конкурента или прибыли. Обычные JSON-отчёты не содержат рекламы.

Архив закреплён за commit `7206178f1f6c7484c6f4463c62fe48d497b398d6`, SHA-256 `c336b9205337f967590378fdb782b654ce9443e3df909e3b1e1aadca11f1b025`. Установка и учебный запуск прошли [четыре CI-проверки](https://github.com/ilookatshow-gif/competitor-offer-radar/actions/runs/38153820165): Ubuntu 24.04/Python 3.9 и 3.12, Windows Server 2022/Python 3.12, macOS 15/Python 3.12. Это проверенные окружения, не гарантия любого агентского клиента. Старый ZIP v0.1.0 не содержит последующего исправления кириллицы.

### English: install the verified source

Download the pinned ZIP above, unpack it and open the module directory in your agent. Python 3.9+ is required; no account, credentials or paid core is needed.

> Read this competitor-offer-radar archive's README.md and AGENTS.md. Install into a new prefix outside the source directory without changing system PATH. Run doctor, tests, validate both synthetic snapshots and compare them. Check declared amounts, delivery and changed scope against the inputs. Run explicit onboard once with a separate local state directory. Do not fetch websites, connect accounts or publish my data. Report missing Python or permissions instead of claiming a successful installation.

Use the commands above, substituting `python` on Windows when appropriate. This is the source revision with the encoding fix, not a replacement for historical v0.1.0. Synthetic results are not commercial outcomes.

Подготовил **Дмитрий Лукашов / Dmitry Lukashov**. [Практические разборы](https://t.me/lookatsoul) · [Научиться на своей задаче](https://lookatshow.ru/executive?utm_source=github&utm_medium=open_module&utm_campaign=catalog&utm_content=start_here_learn) · [Поручить внедрение](https://lookatshow.ru/ai-implementation/?utm_source=github&utm_medium=open_module&utm_campaign=catalog&utm_content=start_here_implementation)
