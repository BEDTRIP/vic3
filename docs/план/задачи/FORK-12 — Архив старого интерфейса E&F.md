---
type: issue
description: "Старые окна E&F и подмены ванильных панелей — в архив; аудит R10 по окнам"
project: vic3
tags: [форк, интерфейс]
kind: task
component: FORK
epic: "[[Этап R10. Интерфейс и графика]]"
date: 2026-11-20
status: todo
aliases: ["R10 шаг 3"]
touches: ["Economic-and-Financial-Ledgerdemain-Mod/gui/", "Economic-and-Financial-Ledgerdemain-Mod/common/scripted_guis/", "Economic-and-Financial-Ledgerdemain-Mod/_archive/"]
depends: ["[[FORK-11 — Перечень окон денег]]"]
---
# FORK-12 — Архив старого интерфейса E&F

По [[ADR-0282 — Старый интерфейс E&F — в архив целиком, новый — заново|ADR-0282]]: `ld_cb_rate_panel.gui`,
`ld_economy_panel.gui`, `00_ef_deported_gui_1/2.gui`, подмены `budget_panel` / `market_panel` / `country_panel` /
`states_panel` / `topbar` — ванильные файлы назад, их scripted_gui, списки (`08_list_effect.txt`), локализация — в
`_archive/` по правилам; описания в столицах. Вместе — аудит R10: С5 окна, С9 `speculative_share_N_button`, остатки
окон E&F по 58 валютам, которых форк не назначает, подмена CMF `00_MPM_building_details_panel.gui`. Подробно —
[[Этап R10. Интерфейс и графика — до задач#Очередь|снимок этапа, «Очередь»]], шаг 3, и [[Этап R10. Интерфейс и графика — до задач#Аудит — закрыть или перенести с причиной|снимок этапа, «Аудит — закрыть или перенести с причиной»]].

## Проверка

- игра грузится без ошибок по `gui/` форка; `v3 lint` без отчётов по снятым файлам

## Ход

- 20.11 — заведена при переводе на задачи ([[DOCS-1 — Перевод документов на метод ca31a1d|DOCS-1]]) из [[Этап R10. Интерфейс и графика — до задач|снимка этапа]].
