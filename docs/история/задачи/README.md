---
type: reference
description: "Закрытые задачи и баги проекта vic3 — ключи и ссылки те же, читать по ссылке"
project: vic3
tags: [история]
---
# Закрытые задачи

Задачи `done` и `wontdo`, закрытые баги ([[История (archive)]]); имя и ключ — те же, что в работе.

```base
filters:
  and:
    - file.inFolder(this.file.folder)
    - type == "issue"
views:
  - type: table
    name: Закрытые
    order:
      - file.name
      - status
      - verified_by
      - description
    sort:
      - property: file.name
        direction: DESC
    rowHeight: tall
    columnSize:
      file.name: 220
      note.status: 80
      note.verified_by: 160
      note.description: 240
```
