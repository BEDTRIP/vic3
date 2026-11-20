---
type: issue
description: "V3 docs check в CI всех репо; workflow в vic3_tools правит пользователь (нет права у токена)"
project: vic3
tags: [инструменты]
kind: task
component: TOOLS
epic: "[[Этап ОБН. Обновление источников]]"
date: 2026-11-20
status: blocked
aliases: ["ОБН шаг 7"]
touches: ["vic3_tools/.github/"]
question: "Добавь в vic3_tools/.github/workflows/ci.yml шаг «- run: v3 docs check» (у токена агента нет права workflow) — или дай токену право workflow, тогда сделаю сам во всех репо"
---
# TOOLS-1 — v3 docs check в CI всех репо

Проверка документов — в CI каждого репо ([[Проверка (docs lint)]]: у правила — исполнитель). В `vic3_tools` —
строка `- run: v3 docs check` в `.github/workflows/ci.yml`; у токена агента нет права `workflow` — правит
пользователь. Остальные репо — по образцу, после того как `v3 docs check` из узла чистый ([[DOCS-1 — Перевод документов на метод ca31a1d|DOCS-1]]). Подробно —
[[Этап ОБН. Обновление источников — до задач#Шаги|снимок этапа, «Шаги»]], шаг 7.

## Проверка

- CI каждого репо падает на находке `v3 docs check`

## Ход

- 20.11 — заведена при переводе на задачи ([[DOCS-1 — Перевод документов на метод ca31a1d|DOCS-1]]) из [[Этап ОБН. Обновление источников — до задач|снимка этапа]].
