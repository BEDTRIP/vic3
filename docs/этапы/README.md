---
type: reference
description: "Папка этапов узла: все открытые этапы проекта vic3 — файл на этап, таблица по шапкам"
project: vic3
tags: [план]
---
# Этапы

Файл на этап, с начала работы: `Этап <номер>. <имя>.md` — [[methodology/Этап|методика]]; порядок и статус — [[план]].
Закрытый — в `история/` с «Итогом».

```base
filters:
  and:
    - file.inFolder(this.file.folder)
    - note.type == "phase"
views:
  - type: table
    name: Этапы
    order:
      - file.name
      - status
      - date
```
