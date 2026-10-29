---
description: "Моды Victoria 3 (Economic-and-Financial-Ledgerdemain и другие): планы и этапы разработки"
status: active
calendar: false
todoist: false
code: C:\ProjectData\vic3
---
## Где мы

## Задачи проекта 10 - Projects/vic3 mods:
```tasks
path includes 10 - Projects/vic3 mods
heading does not include 10 - Projects/vic3 mods:
heading does not include Повторяемое
not done
```
- [ ] Привести документацию к шаблону: в `vic3_mods` — `План проекта.md` → `план.md` + `этапы/<этап>.md` (как в E&F); в остальных проектах, где идёт работа, — так же. Их видят планировщик и дворецкий (`docs_mirror`, раскладка — `docs/documentation.md` zaba-system)
- [ ]
## Решения
```base
filters:
  and:
    - file.inFolder("15 - Open/vic3 mods")
    - note.type == "decision"
properties:
  file.name:
    displayName: Вопрос
  note.description:
    displayName: Что выбрали
  note.status:
    displayName: Статус
views:
  - type: table
    name: Решения проекта
    order:
      - file.name
      - description
      - status
      - date
    sort:
      - property: date
        direction: DESC
```
## Заметки
