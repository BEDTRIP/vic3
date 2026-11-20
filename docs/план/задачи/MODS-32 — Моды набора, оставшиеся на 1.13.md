---
type: issue
description: "Моды набора, оставшиеся на 1.13"
project: vic3
tags: [пачка]
kind: task
component: MODS
epic: "[[Этап П. Пачка]]"
date: 2026-11-20
status: blocked
aliases: ["ОБН.П1"]
touches: ["vic3_mods/"]
question: "Моды набора, оставшиеся на 1.13 (BPM, T&R, LLWA, PSC, TGR Loans): по каждому — 1 оставить на 1.13, 2 снять из набора, 3 ждать автора. Рекомендую решать при пересмотре пачки после форка до 1.15"
---
# MODS-32 — Моды набора, оставшиеся на 1.13

**Моды набора, оставшиеся на 1.13**, перекрывают изменённые в 1.15 записи ваниль: BPM 890 (и 5
убранных: `ideology_social_democrat`, `ideology_socialist`, `social_democrat_party`, `je_canada_gbr`, `je_vanguard`),
T&R 138 (ссылки на убранные `add_war_exhaustion`, `has_war_exhaustion`, `country_war_exhaustion_casualties_mult`,
`can_reach_target_country`; define `NWar.DEVASTATION_INCREASE_RATE` убран), LLWA 16, PSC 7, TGR Loans 2. Решить по
каждому: оставить в наборе на 1.13, снять или ждать автора.

Подробно — [[Этап П. Пачка — до задач#Из отчёта ОБН (12.11)|снимок этапа, «Из отчёта ОБН (12.11)»]].

## Проверка

- `--check` генераторов и `v3 lint` затронутых сборок чистые; в игре — как в описании

## Ход

- 20.11 — заведена при переводе на задачи ([[DOCS-1 — Перевод документов на метод ca31a1d|DOCS-1]]) из [[Этап П. Пачка — до задач|снимка этапа]].
