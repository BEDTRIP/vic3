---
type: reference
description: "История узла: закрытые этапы, снимки прежних файлов этапов, закрытые задачи — читать по ссылке"
project: vic3
tags: [история]
---
# История

Закрытое целиком ([[История (archive)]]): этапы с «Итогом» сверху, снимки (`kind: snapshot`) — прежние файлы этапов до
перевода на задачи 20.11; закрытые задачи — `задачи/`. Историю не переписывают — чинят только ссылки.

```base
filters:
  and:
    - file.inFolder(this.file.folder)
    - type == "history"
views:
  - type: table
    name: История
    order:
      - file.name
      - date
      - kind
      - description
    sort:
      - property: date
        direction: DESC
    rowHeight: tall
    columnSize:
      file.name: 230
      note.date: 90
      note.kind: 80
      note.description: 300
```
