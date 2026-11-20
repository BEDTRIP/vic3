---
type: reference
description: "Папка задач узла: открытые задачи всех репо проекта vic3 — области и их ключи, таблица по шапкам"
project: vic3
tags: [план]
---
# Задачи

Файл на задачу — `<КЛЮЧ-N> — <тема>.md` ([[Задача (issue)]], баг — [[Баг (bug)]]); закрытые — в
`история/задачи/`. Задачи всех репо — здесь, в узле ([[Проект из нескольких репо (polyrepo)]]). Прежний номер пункта
этапа (`ОБН.Ф1`, `МП.9`, `В.R10.5`) — в `aliases`.

## Области

| ключ | область | что |
| --- | --- | --- |
| `FORK` | форк «E&F: Ledgerdemain» | `Economic-and-Financial-Ledgerdemain-Mod/` — механики, интерфейс, графика, выкладка мода |
| `MODS` | пачка | `vic3_mods/` — компачи, мегапаки, аддоны, переводы, ИИ и баланс набора, выкладки сборок |
| `TOOLS` | инструменты | `vic3_tools/` — `v3`, мост `vic3-pc`, плагин навыков, ComfyUI |
| `SRC` | источники | `vic3_mods_out/` — снимок игры и чужих модов, граф документов источников |
| `DOCS` | документы и метод | `docs/` узла, метод, правила агента, уроки |

Новая область — строкой сюда и в `components` настройки проверки узла (`docs-check.toml`).

```base
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
