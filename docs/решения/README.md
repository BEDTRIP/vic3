---
type: reference
description: "Папка решений узла: сквозные решения проекта vic3 — файл на решение, таблица по шапкам"
project: vic3
tags: [решения]
---
# Решения

Сквозные решения проекта — те, что касаются нескольких репо или узла; решения одного репо — в его `docs/решения/`
([[Д.ДОК.3 — документ в репо кода или в узле|Д.ДОК.3]]). Файл — `Д.<этап>.<n> — <тема>.md`, заголовок — вопрос; как
вести — [[methodology/Решение|методика]]. Заменённые — в `история/решения/`.

```base
filters:
  and:
    - file.inFolder(this.file.folder)
    - note.type == "decision"
properties:
  file.name:
    displayName: Решение
  note.status:
    displayName: Статус
  note.date:
    displayName: Когда
views:
  - type: table
    name: Решения
    order:
      - file.name
      - status
      - date
      - by
    sort:
      - property: date
        direction: DESC
```
