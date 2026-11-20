---
type: issue
description: "CMF 1.15"
project: vic3
tags: [форк]
kind: task
component: FORK
epic: "[[Этап Ф. Форк до 1.15]]"
date: 2026-11-20
status: todo
aliases: ["ОБН.Ф5"]
touches: ["Economic-and-Financial-Ledgerdemain-Mod/"]
---
# FORK-5 — CMF 1.15

**CMF 1.15**: CMF больше не дописывает `on_country_formed` (форк дописывает сам —
`common/on_actions/ld_new_country_immediate_init.txt`, проверить, что не опирался на CMF); `annex_country` в
`gui/country_panel.gui` — CMF убрал свою запись с этим ключом, сверить; новые законы полиции CMF
(`law_*_police`) — видны ли в окнах форка.

Из отчёта [«1.13 → 1.15»](https://claude.ai/artifact/HspWQ1dxZhCURL6f27qC3J) — [[Этап ОБН. Обновление источников — до задач#Отчёт «1.13 → 1.15» и задачи из него (шаг 4, 12.11)|снимок этапа, «Отчёт „1.13 → 1.15“ и задачи из него»]].

## Проверка

- `v3 lint`, `v3 conflicts` и прогон форка на 1.15 — без ошибок по затронутым записям

## Ход

- 20.11 — заведена при переводе на задачи ([[DOCS-1 — Перевод документов на метод ca31a1d|DOCS-1]]).
