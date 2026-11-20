---
type: issue
description: "tgr+vc после обновления исходников 30.09"
project: vic3
tags: [пачка]
kind: task
component: MODS
epic: "[[Этап П. Пачка]]"
date: 2026-11-20
status: todo
aliases: ["VC.12"]
touches: ["vic3_mods/"]
depends: ["[[MODS-13 — Судьба TGR в пачке]]"]
---
# MODS-7 — `tgr+vc` после обновления исходников 30.09

**`tgr+vc` после обновления исходников 30.09** (Morgenröte 2.8.3k, VC, TGR, grey_soft_pop): `py
tools/regen_vc_tgr.py --check --only <раздел>` — расхождение в `companies` (VC срезал бонусы 29 компаниям),
`interest_groups` (TGR закомментировал `IN_GOVERNMENT_ATTRACTION`), `pop_needs` (TGR: `max_supply_share` 0.3 → 0.25,
табак, новый `popneed_stimulants` — REPLACE VC его стирает), `history` (опиум). Каскад: аддон-VC, `greys+vc`,
`greys+addon-vc`, `--check` у `regen_greys_vc.py`, `regen_addon_vc.py`. **Зависит от [[MODS-13 — Судьба TGR в пачке|MODS-13]]:** если TGR уходит из
пачки — задача снимается вместе с `tgr+vc`.

Подробно — [[Этап П. Пачка — до задач#П0. Текущее|снимок этапа, «П0. Текущее»]].

## Проверка

- `--check` генераторов и `v3 lint` затронутых сборок чистые; в игре — как в описании

## Ход

- 20.11 — заведена при переводе на задачи ([[DOCS-1 — Перевод документов на метод ca31a1d|DOCS-1]]) из [[Этап П. Пачка — до задач|снимка этапа]].
