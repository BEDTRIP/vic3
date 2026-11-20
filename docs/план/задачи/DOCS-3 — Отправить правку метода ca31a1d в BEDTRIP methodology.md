---
type: issue
description: "Отправить правку метода с правилами vic3 в BEDTRIP/methodology — нет записи у токена"
project: vic3
tags: [документация]
kind: task
component: DOCS
epic: "[[Документация]]"
date: 2026-11-20
status: blocked
touches: ["репо methodology на GitHub"]
question: "Дай токену рабочего запись в BEDTRIP/methodology (тогда отправлю сам) — или отправь патч _tmp_analysis/methodology-ca31a1d.patch (два коммита: ca31a1d, 8442e0a): git am и git push"
---
# DOCS-3 — Отправить правку метода ca31a1d в BEDTRIP/methodology

Правила vic3 (узел — «Проект из нескольких репо (polyrepo)», документ кода мода по подсистемам, язык публичного репо,
поток) внесены в метод коммитом ca31a1d; копия в узле — с него. В `BEDTRIP/methodology` он не отправлен: у токена
рабочего нет записи (403). Второй коммит — 8442e0a: `audience` — только метка фильтра, на агентские заметки ссылаются как на любые (пользователь 20.11). Патч обоих — `_tmp_analysis/methodology-ca31a1d.patch` узла.

Заодно — в метод: в «Перевод проекта на методологию (migration guide)» ссылка `[[README|…]]` в хранилище из
нескольких репо неоднозначна (у каждой папки свой README) — нужен путь `[[methodology/README|…]]` или имя карты метода;
пока — в `docs-check-known.txt` узла.

## Проверка

- ca31a1d — в `main` `BEDTRIP/methodology`; копия метода в узле совпадает с ним

## Ход

- 20.11 — заведена при переводе на задачи ([[DOCS-1 — Перевод документов на метод ca31a1d|DOCS-1]]).
- 20.11 — в метод добавлен 8442e0a (audience — метка фильтра); копия в узле — с него; патч — оба коммита.
