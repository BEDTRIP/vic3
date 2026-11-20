---
type: issue
description: "Экономика 1.15 под модель форка"
project: vic3
tags: [форк]
kind: task
component: FORK
epic: "[[Этап Ф. Форк до 1.15]]"
date: 2026-11-20
status: todo
aliases: ["ОБН.Ф4"]
touches: ["Economic-and-Financial-Ledgerdemain-Mod/"]
---
# FORK-4 — Экономика 1.15 под модель форка

**Экономика 1.15 под модель форка**: `NEconomy.BUILDING_PROFIT_TARGET_TO_HIRE_EMPLOYEES` 0,25 → 0,15,
`…_TO_RAISE_WAGES` 0,25 → 0,20, `…_TO_LOWER_WAGES` 0,15 → 0,10, `…_TO_WITHDRAW_CASH` 0,15 → 0,10,
`BUILDING_WAGES_AVERAGE_PRODUCTIVITY_THRESHOLD` 0,5 → 0,75; новые `NAI.MONEY_SPENDING_CONSTRUCTION_MAX_INVESTMENT_POOL_WEEKS`,
`NAI.GOVERNMENT_WAGE_LEVEL_CHANGES_ENABLED` и др.; убраны `NAI.PRODUCTION_BUILDING_AUTONOMOUS_INVESTMENT_BELOW_DESIRED_INFRASTRUCTURE_FACTOR_MULT` и `…_LOW_INVESTMENT_RESET_TIME`,
`NEconomy.BUILDING_MAX_PROFIT_TO_PAUSE_HIRES`, `PEASANT_STARTING_WAGE_RATE_FACTOR`. Сверить с понятиями форка
(касса предприятий, пул инвестиций) — прогоном 1.15.

Из отчёта [«1.13 → 1.15»](https://claude.ai/artifact/HspWQ1dxZhCURL6f27qC3J) — [[Этап ОБН. Обновление источников — до задач#Отчёт «1.13 → 1.15» и задачи из него (шаг 4, 12.11)|снимок этапа, «Отчёт „1.13 → 1.15“ и задачи из него»]].

**1.15.2 ([[SRC-6 — Снимок источников и граф на 1.15.2|SRC-6]]):** defines `NAI` — `AUTONOMOUS_INVESTMENT_COMPANY_TARGET_BUILDING_TYPE_CONSTRUCTION_FACTOR` 5 → 20 (выбор зданий автономных инвестиций компаний), новые `PRODUCTION_METHOD_EMPLOYMENT_CHANGE_NO_AVAILABLE_LABOR_MULT`, `…_ABUNDANT_LABOR_FRACTION`, `PRODUCTION_METHOD_SCORING_OVERRIDE_FACTOR`; `NEconomy` в 1.15.2 не менялся.

## Проверка

- `v3 lint`, `v3 conflicts` и прогон форка на 1.15 — без ошибок по затронутым записям

## Ход

- 20.11 — заведена при переводе на задачи ([[DOCS-1 — Перевод документов на метод ca31a1d|DOCS-1]]).
- 20.11 — уточнена по снимку 1.15.2 ([[SRC-6 — Снимок источников и граф на 1.15.2|SRC-6]]).
