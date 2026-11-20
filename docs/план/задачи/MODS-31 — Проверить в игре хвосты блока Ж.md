---
type: issue
description: "Проверить в игре"
project: vic3
tags: [пачка]
kind: task
component: MODS
epic: "[[Этап П. Пачка]]"
date: 2026-11-20
status: todo
aliases: ["ВЫК.5"]
touches: ["vic3_mods/", "мастерская Steam"]
---
# MODS-31 — Проверить в игре хвосты блока Ж

**Проверить в игре** (хвосты прежнего блока Ж, что относится к пачке): CMF 02.09 — панель персонажа не
дерётся с Morgenröte; VC chi29 — нет `Duplicated event ID 'joi_flavor_chi.29'`; значки в лаунчере у
`Addon: Grey's x MegaComPatch`, `ComPatch Grey's + addon-VC`, `ComPatch Grey's + Victorian Century`; жёлтая
«зависимость не в наборе» у `greys+addon-vc`; `TEST_SKIP_EF_GROUPS` (`regen_addon_greys.py`) — пересмотреть под форк.

Подробно — [[Этап П. Пачка — до задач#П5. Выкладка|снимок этапа, «П5. Выкладка»]].

## Проверка

- `--check` генераторов и `v3 lint` затронутых сборок чистые; в игре — как в описании

## Ход

- 20.11 — заведена при переводе на задачи ([[DOCS-1 — Перевод документов на метод ca31a1d|DOCS-1]]) из [[Этап П. Пачка — до задач|снимка этапа]].
