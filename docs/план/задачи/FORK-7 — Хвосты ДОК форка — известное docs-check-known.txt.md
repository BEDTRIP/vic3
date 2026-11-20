---
type: issue
description: "Разобрать известное v3 docs check форка: понятия старого вида без status, номера в коде без ADR"
project: vic3
tags: [форк, документация]
kind: task
component: FORK
epic: "[[Этап Ф. Форк до 1.15]]"
date: 2026-11-20
status: todo
touches: ["Economic-and-Financial-Ledgerdemain-Mod/docs/", "Economic-and-Financial-Ledgerdemain-Mod/docs-check-known.txt"]
---
# FORK-7 — Хвосты ДОК форка — известное docs-check-known.txt

Разобрать `docs-check-known.txt` форка (около 260 строк): понятия старого вида без `status` (разбор «Что в коде» на
«Где» и «Открыто»), номера в коде без ADR, сироты. По каждому — поправить или оставить с причиной; файл должен
худеть, а не расти.

## Проверка

- в `docs-check-known.txt` форка — только строки с причиной, которые остаются осознанно

## Ход

- 20.11 — заведена при переводе на задачи ([[DOCS-1 — Перевод документов на метод ca31a1d|DOCS-1]]).
