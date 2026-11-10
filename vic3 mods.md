---
description: "Моды Victoria 3 (Economic-and-Financial-Ledgerdemain и другие): планы и этапы разработки"
status: active
calendar: false
todoist: false
code: C:\ProjectData\vic3
---
## Где мы
Хобби: моды Victoria 3 — свой форк E&F «Ledgerdemain» (деньги, валюты, банки, биржа, облигации), пачка компачей, аддонов и переводов, инструменты `v3`. План и этапы — `docs/план.md` узла.

- **Документация** переведена на методику (этап ДОК закрыт 7.11): план и этапы — в узле, понятия и решения — в репо, граф ваниль и 25 модов — генератом `v3 graph`.
- **Сейчас — этап ОБН** (ночь 11.11): игра уже 1.15 — снимок ванили и модов в `vic3_mods_out` на 1.15, граф заново, отчёт «1.13 → 1.15», пилот механик «стройка».
- **Дальше — форк до 1.15** (его зависимости CMF и ETF уже на 1.15), потом этапы R10 (интерфейс и графика), R11 (баланс), R12 (выкладка), R13 (нацзапас).
- **Пачка** — после форка: компачи и переводы под 1.15, пересмотр ребаланса компачей (этап П).

## Задачи проекта 15 - Open/vic3 mods:
```tasks
path includes 15 - Open/vic3 mods
heading does not include 15 - Open/vic3 mods:
heading does not include Повторяемое
not done
```
- [ ] Этап ОБН: источники и граф на 1.15, отчёт «1.13 → 1.15»
- [ ] Форк до 1.15
- [ ] Форк: R10 интерфейс и графика → R11 баланс → R12 выкладка → R13 нацзапас
- [ ] Пачка под 1.15: компачи и локализации
	- [ ] Пересмотреть ребаланс для компачей
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
