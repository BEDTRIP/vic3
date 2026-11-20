---
type: issue
description: "Генераторы на новых инструментах"
project: vic3
tags: [пачка]
kind: task
component: MODS
epic: "[[Этап П. Пачка]]"
date: 2026-11-20
status: todo
aliases: ["ИНСТ.2"]
touches: ["vic3_mods/"]
---
# MODS-4 — Генераторы на новых инструментах

**Генераторы на новых инструментах** (после переезда в `vic3_tools` 15–16.10): все `tools/regen_*.py` и
`build_addon_*.py` с `--check` проходят (парсер — `vic3tools.legacy`, `vic3tools.core.merge3`); упавшие — починить
или пометить `# RETIRED` (`regen_ef_tr_copies.py` уже). HC — отдельно, [[MODS-5 — Копии TGR VC в HC-ветке устарели|MODS-5]]. Проверки сборок — `v3 audit replace
--declared tools/replace_declared.toml`, `v3 audit dups`, `v3 lint` по каждой сборке (база известных отчётов — в корне
сборки).

Подробно — [[Этап П. Пачка — до задач#П0. Текущее|снимок этапа, «П0. Текущее»]].

## Проверка

- `--check` генераторов и `v3 lint` затронутых сборок чистые; в игре — как в описании

## Ход

- 20.11 — заведена при переводе на задачи ([[DOCS-1 — Перевод документов на метод ca31a1d|DOCS-1]]) из [[Этап П. Пачка — до задач|снимка этапа]].
