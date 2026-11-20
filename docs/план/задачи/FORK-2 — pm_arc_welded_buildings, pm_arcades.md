---
type: issue
description: "pm_arc_welded_buildings, pm_arcades"
project: vic3
tags: [форк]
kind: task
component: FORK
epic: "[[Этап Ф. Форк до 1.15]]"
date: 2026-11-20
status: todo
aliases: ["ОБН.Ф2"]
touches: ["Economic-and-Financial-Ledgerdemain-Mod/"]
---
# FORK-2 — `pm_arc_welded_buildings`, `pm_arcades`

**`pm_arc_welded_buildings`, `pm_arcades`** (изменены `building_modifiers`), `static_modifiers/base_values`
— форк перекрывает копией 1.13: трёхстороннее слияние.

Из отчёта [«1.13 → 1.15»](https://claude.ai/artifact/HspWQ1dxZhCURL6f27qC3J) — [[Этап ОБН. Обновление источников — до задач#Отчёт «1.13 → 1.15» и задачи из него (шаг 4, 12.11)|снимок этапа, «Отчёт „1.13 → 1.15“ и задачи из него»]].

**1.15.2 ([[SRC-6 — Снимок источников и граф на 1.15.2|SRC-6]]):** `pm_arc_welded_buildings` изменён ещё раз — `goods_input_tools_add` 30 → 35, `goods_input_copper_add` 10 → 5 (форк — `common/production_methods/zz_PSC_construction.txt`).

## Проверка

- `v3 lint`, `v3 conflicts` и прогон форка на 1.15 — без ошибок по затронутым записям

## Ход

- 20.11 — заведена при переводе на задачи ([[DOCS-1 — Перевод документов на метод ca31a1d|DOCS-1]]).
- 20.11 — уточнена по снимку 1.15.2 ([[SRC-6 — Снимок источников и граф на 1.15.2|SRC-6]]).
