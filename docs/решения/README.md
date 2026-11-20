---
type: reference
description: "Папка ADR узла: сквозные решения проекта vic3 — файл на решение, таблица по шапкам"
project: vic3
tags: [решения]
---
# Решения

Сквозные ADR проекта — те, что касаются нескольких репо или узла; ADR одного репо — в его `docs/решения/`
([[ADR-0301 — документ в репо кода или в узле|ADR-0301]]). Файл — `ADR-NNNN — <тема>.md`, номер сквозной по всем репо,
прежний (`Д.ДОК.12`) — в `aliases`; заголовок — вопрос; как вести — [[Решение (ADR)]]. Заменённые — в
`история/решения/`.

```base
filters:
  and:
    - file.inFolder(this.file.folder)
    - type == "adr"
views:
  - type: table
    name: ADR
    order:
      - file.name
      - aliases
      - status
      - description
    sort:
      - property: file.name
        direction: DESC
    rowHeight: tall
    columnSize:
      file.name: 230
      note.aliases: 90
      note.status: 80
      note.description: 300
```
