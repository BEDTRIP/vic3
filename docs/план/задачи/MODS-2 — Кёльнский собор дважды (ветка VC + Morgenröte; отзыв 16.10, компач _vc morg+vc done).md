---
type: issue
description: "Кёльнский собор дважды (ветка VC + Morgenröte; отзыв 16.10, компач _vc/morg+vc done)"
project: vic3
tags: [пачка]
kind: task
component: MODS
epic: "[[Этап П. Пачка]]"
date: 2026-11-20
status: todo
aliases: ["VC.13"]
touches: ["vic3_mods/"]
---
# MODS-2 — Кёльнский собор дважды (ветка VC + Morgenröte; отзыв 16.10, компач `_vc/morg+vc done`)

**Кёльнский собор дважды (ветка VC + Morgenröte; отзыв 16.10, компач `_vc/morg+vc done`).** VC — дневник
`restore_cologne_cathedral` (`VC: common/journal_entries/prussia_kingdom.txt`:1033, одна кнопка и ожидание;
`on_complete` ставит `restore_cologne_cathedral_complete_var`, :1073), его читает требование «Консервативный порядок:
пиетизм» (`conservative_order_prussia_religious`, :878). Morgenröte — решение и цепочка событий со стройкой в фазах,
здание `building_gaudi_dom` (`Morgenrote: common/buildings/mr_arts_gaudi_monuments.txt`:11, строит `gaudi.108`,
`events/arts/gaudi_events.txt`:4167). Предложение игрока: завершение Morgenröte засчитывать пиетизму, дневник VC убрать.
План: в `morg+vc` — `is_shown` / `possible` дневника VC ложны при Morgenröte, глобальная переменная ставится при
постройке собора Morgenröte (`gaudi.108` или `on_building_built`), подсказка требования пиетизма — про собор
Morgenröte. Проверить, нет ли других пересечений «памятник дважды» VC × Morgenröte (`v3 refs` по `restore_*` VC против
зданий `gaudi` / `mr_arts_*`). Пересобрать мегапак / аддон-VC, если файл там.

Подробно — [[Этап П. Пачка — до задач#П0. Текущее|снимок этапа, «П0. Текущее»]].

## Проверка

- `--check` генераторов и `v3 lint` затронутых сборок чистые; в игре — как в описании

## Ход

- 20.11 — заведена при переводе на задачи ([[DOCS-1 — Перевод документов на метод ca31a1d|DOCS-1]]) из [[Этап П. Пачка — до задач|снимка этапа]].
