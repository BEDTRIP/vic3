---
type: issue
description: "Справочник движка 1.15"
project: vic3
tags: [форк]
kind: task
component: FORK
epic: "[[Этап Ф. Форк до 1.15]]"
date: 2026-11-20
status: todo
aliases: ["ОБН.Ф6"]
touches: ["Economic-and-Financial-Ledgerdemain-Mod/"]
depends: ["[[SRC-1 — Дамп движка 1.15 и справочник движка]]"]
---
# FORK-6 — Справочник движка 1.15

**Справочник движка 1.15**: после дампа (Д.ОБН.7) — `v3 refs` эффектов, триггеров и модификаторов
форка против справочника 1.15 (убраны, судя по `common/`: `add_war_exhaustion`, `damage_ship*`,
`country_war_exhaustion_casualties_mult`).

Из отчёта [«1.13 → 1.15»](https://claude.ai/artifact/HspWQ1dxZhCURL6f27qC3J) — [[Этап ОБН. Обновление источников — до задач#Отчёт «1.13 → 1.15» и задачи из него (шаг 4, 12.11)|снимок этапа, «Отчёт „1.13 → 1.15“ и задачи из него»]].

## Проверка

- `v3 lint`, `v3 conflicts` и прогон форка на 1.15 — без ошибок по затронутым записям

## Ход

- 20.11 — заведена при переводе на задачи ([[DOCS-1 — Перевод документов на метод ca31a1d|DOCS-1]]).
