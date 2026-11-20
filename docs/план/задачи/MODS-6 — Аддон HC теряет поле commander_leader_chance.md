---
type: issue
description: "Аддон HC теряет поле"
project: vic3
tags: [пачка]
kind: task
component: MODS
epic: "[[Этап П. Пачка]]"
date: 2026-11-20
status: todo
aliases: ["HC.15"]
touches: ["vic3_mods/"]
depends: ["[[MODS-5 — Копии TGR VC в HC-ветке устарели]]"]
---
# MODS-6 — Аддон HC теряет поле commander_leader_chance

**Аддон HC теряет поле** (`v3 audit replace`, 15.10): `__addon/addon hc+gob+moh/common/interest_groups/
zz_hct_ig_rural_folk.txt`:45 `REPLACE:ig_rural_folk` без `commander_leader_chance` из тела HC (`for addon/Hail
Columbia/common/interest_groups/00_rural_folk.txt`:1). Вернуть поле в генераторе аддона либо внести в
`tools/replace_declared.toml` с причиной. Вместе с [[MODS-5 — Копии TGR VC в HC-ветке устарели|MODS-5]].

Подробно — [[Этап П. Пачка — до задач#П0. Текущее|снимок этапа, «П0. Текущее»]].

## Проверка

- `--check` генераторов и `v3 lint` затронутых сборок чистые; в игре — как в описании

## Ход

- 20.11 — заведена при переводе на задачи ([[DOCS-1 — Перевод документов на метод ca31a1d|DOCS-1]]) из [[Этап П. Пачка — до задач|снимка этапа]].
