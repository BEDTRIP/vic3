---
type: explanation
description: "Раскладка документов проекта: docs/ и его папки, план/ с этапами и задачами, файл папки README.md, документ кода рядом с кодом, что не документ"
project: methodology
aliases: [Где лежит]
tags: [методология]
status: done
---
# Где лежит (docs layout)

## Суть

Общие знания проекта — в `docs/` в корне репозитория, документ кода — рядом с кодом. Что за документ и к чему он
относится, говорит [[Шапка документа (frontmatter)|шапка]], а не папка; папки постоянны только там, где по ним что-то находят
инструменты.

## Правила

```
docs/
  README.md            вход (entry) и файл папки docs/
  methodology/         метод документации целиком, README.md — его карта
  понятия/             понятия и карта понятий (MOC)
  план/                README.md — план (roadmap); рядом — файлы этапов (epic)
    задачи/            открытые задачи (issue: task и bug); README.md — области и их ключи
  решения/             ADR
  уроки/               уроки (lessons learned)
  devices/<устройство>/  всё об устройстве: карточка, справочник, обслуживание
  история/             закрытые этапы и снимки (archive); задачи/ — закрытые задачи, решения/ — заменённые и
                       отменённые ADR
  *.md, <подсистема>/  процедуры (how-to) и справочники (reference)
  attachments/         картинки и схемы документов
  *.base               виды Obsidian (таблицы по шапкам) — не документы
```

- **Файл папки** — `README.md` в каждой папке документов (`type: reference`): что в папке и как туда класть. У папки
  однотипных документов (ADR, задачи, история) — таблица Bases по шапкам вместо оглавления; фильтр —
  `file.inFolder(this.file.folder)`, не путь: так таблица работает, где бы папка ни лежала. В Obsidian файл папки
  открывается щелчком по папке — плагин «Folder Notes» с именем заметки папки `README`; это тот же `README.md`, что у
  папки кода: один файл и для git, и для Obsidian. Исключения — `понятия/` и `methodology/`: их вход — карта
  ([[Понятие (explanation)#Карта]]); у `план/` файл папки — сам план.
- [[Документ кода (module README)]] — `README.md` в папке модуля. `README.md` в корне репозитория — вход в репозиторий (`entry`): что
  за проект, как начать, ссылка на вход `docs/`; процедуры из него — в `docs/`.
- Имя папки `план/` постоянное: по нему инструменты находят документы планирования. Остальное — как удобно.
- **Проект из нескольких репо** — узел над ними: план, этапы, задачи и сквозное — в его `docs/`, остальное — в `docs/`
  своего репо ([[Проект из нескольких репо (polyrepo)]]).
- **Списки — виды по шапкам.** Оглавлений, хронологий, таблиц задач, ADR и очередей руками не ведут — их строят виды
  Obsidian (Bases) по шапкам: список, который пишут руками, отстаёт с первой правкой.
- **Таблица — под ширину заметки.** Четыре колонки: имя первой, `description` последней, между ними — то, ради чего
  таблицу открывают (статус и чего ждёт; что проверить; чем принято); остальное человек добавляет сам кнопкой
  «Свойства». Строки высокие (`rowHeight: tall`) — описание читается целиком; ширины заданы (`columnSize`), в сумме
  около 700 — без прокрутки вбок. Новая таблица — копией образца ([[#Образцы таблиц]]), а не с нуля.
- Файлы, которые собирает скрипт и которые не Markdown (`csv`, `json`), шапки не имеют — их описывает справочник
  рядом, с `generated` ([[Процедура и справочник (how-to, reference)]]). Картинка — в `attachments/`, имя — о чём она, не номер.
- **Не документы** — разметка документов им не ставится, [[Проверка (docs lint)]] их пропускает: правила работы агента и проекта
  (`CLAUDE.md`, `AGENTS.md`, навыки), данные и шаблоны, которые проект выкладывает в чужие места (у них разметка того
  места), тестовые данные и фикстуры, наборы для замеров. Какие папки это — в настройке скрипта проверки проекта.
  В графе Obsidian им — своя группа цвета (по папке или тегу): их острова и сироты — норма, не дефект ссылок. Новая
  папка не-документов — в обе настройки.

## Образцы таблиц

В документе блок открывается строкой `` ```base ``; здесь он показан как `yaml`, чтобы образец не строился таблицей.

**Задачи этапа** — в файле [[Этап (epic)|этапа]], раздел «Задачи»: задачи, которые ссылаются на этап (`epic`).

```yaml
filters:
  and:
    - type == "issue"
    - file.hasLink(this.file)
views:
  - type: table
    name: Открытые
    filters:
      and:
        - status != "done"
        - status != "wontdo"
        - status != "verified"
        - status != "invalid"
        - status != "duplicate"
        - status != "wontfix"
    groupBy:
      property: status
      direction: ASC
    order:
      - file.name
      - question
      - answer
      - description
    sort:
      - property: date
        direction: ASC
    rowHeight: tall
    columnSize:
      file.name: 180
      note.question: 190
      note.answer: 130
      note.description: 200
  - type: table
    name: Архив
    filters:
      or:
        - status == "done"
        - status == "wontdo"
        - status == "verified"
        - status == "invalid"
        - status == "duplicate"
        - status == "wontfix"
    order:
      - file.name
      - status
      - verified_by
      - description
    sort:
      - property: date
        direction: DESC
    rowHeight: tall
    columnSize:
      file.name: 200
      note.status: 90
      note.verified_by: 160
      note.description: 250
```

**Файл папки** однотипных документов — `README.md` папки; `type` — вид документов папки, средние колонки — по нему
(у ADR — номер и `status`, у уроков — `applies`, у истории — `date` и `kind`).

```yaml
filters:
  and:
    - file.inFolder(this.file.folder)
    - type == "issue"
views:
  - type: table
    name: По этапам
    groupBy:
      property: epic
      direction: ASC
    order:
      - file.name
      - status
      - question
      - answer
      - description
    sort:
      - property: status
        direction: ASC
      - property: date
        direction: ASC
    rowHeight: tall
    columnSize:
      file.name: 170
      note.status: 90
      note.question: 160
      note.answer: 110
      note.description: 170
```

Ключ ширины — как колонка названа в `order`: свойство шапки — с `note.` (`note.status`), имя файла — `file.name`,
формула — `formula.<имя>`.
