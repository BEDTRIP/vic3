---
type: issue
description: "Ссылки компачей на убранное в 1.15"
project: vic3
tags: [пачка]
kind: task
component: MODS
epic: "[[Этап П. Пачка]]"
date: 2026-11-20
status: todo
aliases: ["ОБН.П3"]
touches: ["vic3_mods/"]
---
# MODS-34 — Ссылки компачей на убранное в 1.15

**Ссылки компачей на убранное в 1.15**: `ideology_social_democrat` / `ideology_socialist` /
`social_democrat_party` (`addon vc`, `addon llwa`, `tgr+vc`, `llwa+kai`); триггеры ИИ `can_reach_target_country`,
`can_reach_target_state`, `ai_desires_target_state`, `ai_strongly_desires_target_state` (`addon greys`,
`addon hc+gob+moh`, `greys_kai_fix`, `hc+kai`) — заменить на ключи 1.15 или убрать.

Подробно — [[Этап П. Пачка — до задач#Из отчёта ОБН (12.11)|снимок этапа, «Из отчёта ОБН (12.11)»]].

## Проверка

- `--check` генераторов и `v3 lint` затронутых сборок чистые; в игре — как в описании

## Ход

- 20.11 — заведена при переводе на задачи ([[DOCS-1 — Перевод документов на метод ca31a1d|DOCS-1]]) из [[Этап П. Пачка — до задач|снимка этапа]].
