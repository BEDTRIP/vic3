---
type: how-to
description: "Как написать скрипт проверки документации под проект: что считать документом, как разрешать ссылки как Obsidian, упоминания и --fix, paths и verified; образец ядра на Python"
project: methodology
aliases: [Скрипт проверки]
tags: [методология]
---
# Скрипт проверки (linter)

Скрипт держит правила [[Проверка (docs lint)|проверки]]. **Пишет его агент проекта** под его раскладку — одна команда, код выхода 1
при находках. Как устроить:

- Документы — все `.md` проекта, кроме «не документов» (список папок — в начале скрипта). Пути ссылок считаются от
  корня хранилища Obsidian — обычно это корень репозитория.
- Ссылки искать вне кода: блоки кода и `` `…` `` вырезать до поиска — там примеры. В строке таблицы `|`
  в ссылке пишется `\|`.
- Ссылки Markdown `[текст](путь)` без схемы (`https:`) Obsidian тоже разрешает как заметки — не нашёл, в графе
  фантомный узел; их проверять так же (образец в тексте — в `` `…` ``).
- Часть документов копируется в другое хранилище — ссылки из неё на остальное там будут фантомами, это допустимо.
  Какие ссылки копируемой части запрещены (например, понятиям — только на скопированное рядом) — правило проекта
  в его скрипте.
- Ссылку разрешать так, как Obsidian (`resolve` и `pick` в образце), а не «есть ли файл с таким именем»: иначе не
  видно ссылок, которые ведут не туда. Регистр не различать — на Windows и macOS Obsidian его не различает.
- Упоминания текстом — регулярными выражениями по видам: «ADR-N», ключ задачи, «этап N», путь к документу в
  `` `…` ``, имя понятия (длинные имена первыми, только первое упоминание в документе); до поиска вырезать шапку,
  код и уже стоящие ссылки. С `--fix` скрипт заменяет найденное ссылкой; историю не переписывает.
- История (`история/`) — только ссылки и якоря: шапки внутри и упоминания текстом там остаются как были ([[История (archive)]]).
- Ссылки из кода: в файлах кода (по расширениям) искать в комментариях ключи задач, номера ADR и пути к `.md`;
  ключ или номер — есть ли документ с таким началом имени в `план/задачи/`, `решения/` или их истории; путь — существует ли файл
  ([[Документ кода (module README)]]).
- Скрипт — в CI отдельной проверкой, которая роняет сборку при находках: проверка, которую запускают по памяти, через
  месяц не запускают.
- `verified` и `paths` — через git: дата последнего коммита по маскам из `paths`
  (`git log -1 --format=%cs -- <маска>`) позже даты в `verified` — «возможно, устарел».
- [[Задача (issue)|Задачи]] — после прохода по документам, когда шапки всех собраны: `depends` разрешать как ссылку и
  смотреть `type` цели; в `touches` путь — то, что с `/` или с расширением, остальное — общий ресурс, его не
  проверять, но сравнивать; пересечение — тот же ресурс или путь внутри пути. Закрытую задачу в истории не проверять
  на пути.
- Протухшая заявка — тоже через git: время последнего коммита по файлу задачи (`git log -1 --format=%ct -- <файл>`)
  старше срока проекта. Заявка сама — коммит, отдельно сравнивать с `claimed` нужно только для незакоммиченного.
- Сроки и пороги (срок заявки, размер файла этапа и задачи, возраст «Состояния» плана) — константами в начале
  скрипта. То, что чинит уборка, а не автор коммита, — протухшая заявка, пересечение, размер, возраст «Состояния» —
  справочно: иначе чужая заявка остановит коммит всем.
- Таблицы: строка — та, что начинается с `|`; заголовок — строка, за которой идёт разделитель `| --- |`; ячейки
  считать по `|` без `\` перед ним, шапку и блоки кода до этого вырезать с сохранением номеров строк. Чаще всего
  лишнюю ячейку даёт `[[док|подпись]]` без `\|`.
- Правила — функциями от данных (шапки, «сейчас», «есть ли путь»), а не от диска и git: тогда на каждое правило
  есть тест на выдуманных шапках.
- Документы с `generated` `--fix` не трогает: следующая сборка перепишет их обратно, и две программы будут спорить.
- Файлы писать в UTF-8 с теми же концами строк, что были, — иначе дифф на весь файл.
- Разрешение ссылок кешировать: оно зовётся на каждое имя в каждом куске текста.
- Вывод — строка на находку «файл: что не так»; отдельно «справочно» — то, что не ошибка (одно имя у двух
  документов, код ни в одном `paths`).

**Образец ядра** — шапки, ссылки, якоря, таблицы, задачи (Python 3.8+). Дописать под проект: карта и «Суть» понятий,
упоминания текстом и `--fix`, `paths`, `verified`, правила багов, ссылки из кода, возраст «Состояния» плана.

```python
"""Проверка документации — ядро: шапки, ссылки, якоря, таблицы, задачи. Код выхода 1 — есть находки."""
import re, subprocess, sys, time
from pathlib import Path
from urllib.parse import unquote

ROOT = Path(sys.argv[1]) if len(sys.argv) > 1 else Path(__file__).resolve().parent.parent   # корень хранилища
SKIP = {".git", ".obsidian", ".trash", "node_modules", ".venv"}   # и папки «не документов» проекта
TYPES = {"entry", "explanation", "moc", "code", "how-to", "reference", "roadmap", "epic", "issue", "adr",
         "lesson", "history"}
TASK = {"todo", "in-progress", "blocked", "review", "done", "wontdo"}
BUG = {"unconfirmed", "confirmed", "in-progress", "blocked", "fixed", "verified", "wontfix", "invalid", "duplicate"}
CLOSED = {"done", "wontdo", "verified", "wontfix", "invalid", "duplicate"}
STATUS = {"explanation": {"open", "done"}, "epic": {"todo", "in-progress", "on-hold", "done"},
          "issue": TASK | BUG, "adr": {"accepted", "superseded", "deprecated"}}
LINK = re.compile(r"!?\[\[([^\]|#\n]*)(?:#([^\]|\n]*?))?(?:\\?\|[^\]\n]*)?\]\]")   # в таблице «|» пишут «\|»
CODE = re.compile(r"```.*?```|`[^`\n]*`", re.S)   # ссылки в коде — примеры, не ссылки
CLAIM_HOURS, SIZE_KB = 24, {"epic": 10, "issue": 8}   # срок заявки и пороги рабочих файлов — свои у проекта


def frontmatter(text):
    m = re.match(r"---\n(.*?)\n---", text, re.S)
    return dict(re.findall(r"^([A-Za-z_]+):[ \t]*(.*?)[ \t]*$", m.group(1), re.M)) if m else None


def items(v):   # значение-список из шапки: ["a/", "[[Задача (issue)]]"] -> [a/, [[Задача (issue)]]]
    return [x.strip().strip('"') for x in re.findall(r'"[^"]*"|[^,\[\]]+', v or "") if x.strip()]


def cells(line):   # ячеек в строке таблицы; «|» внутри ячейки пишут «\|»
    s = line.strip()[1:]
    return len(re.split(r"(?<!\\)\|", s[:-1] if s.endswith("|") and not s.endswith("\\|") else s))


def anchors(text):   # куда может вести [[док#…]]: заголовки и метки блоков ^id
    t = re.sub(r"```.*?```", "", text, flags=re.S)
    return ({h.strip() for h in re.findall(r"^#{1,6} (.+?)\s*$", t, re.M)},
            set(re.findall(r"\s\^([A-Za-z0-9-]+)\s*$", t, re.M)))


files = [p for p in ROOT.rglob("*") if p.is_file() and not SKIP & set(p.relative_to(ROOT).parts)]
known = {p.relative_to(ROOT).as_posix().lower(): p for p in files}   # регистр не различается (Windows, macOS)


def resolve(t):
    """Кандидаты для [[t]], как их ищет Obsidian: файл с таким именем один — он; точный путь от корня — он; иначе все,
    чей путь кончается на t (без расширения в ссылке — только .md)."""
    o = t.replace("\\", "").strip().lower().lstrip("/")
    name = o.rsplit("/", 1)[-1]
    cands = [k for k in known if k.rsplit("/", 1)[-1] in (name + ".md", name if "." in name else None)]
    if "/" not in o and len(cands) == 1:
        return cands
    for x in (o, o + ".md"):
        if x in known:
            return [x]
    return [k for k in cands if k.endswith("/" + o) or k.endswith("/" + o + ".md")]


def pick(cands, src):   # порядок Obsidian: сначала лежащие в папке ссылающегося, потом короче путь
    folder = src.rsplit("/", 1)[0] + "/" if "/" in src else ""
    return sorted(cands, key=lambda k: (not (folder and k.startswith(folder)), len(k)))


sys.stdout.reconfigure(encoding="utf-8")
bad, notes, tasks = [], [], {}   # notes — справочно: чинит уборка, коммит не останавливают
for p in (p for p in files if p.suffix == ".md"):
    r = p.relative_to(ROOT).as_posix()
    text = p.read_text(encoding="utf-8").replace("\r\n", "\n")
    fm = frontmatter(text)
    if fm is None:
        bad.append(f"{r}: нет шапки")
        continue
    bad += [f"{r}: нет {k}" for k in ("type", "description", "project") if not fm.get(k)]
    t = fm.get("type")
    if t and t not in TYPES:
        bad.append(f"{r}: type {t} — не из списка")
    if t in STATUS and fm.get("status") not in STATUS[t]:
        bad.append(f"{r}: status {fm.get('status')} — не из списка для {t}")
    body = CODE.sub("", text)
    bad += [f"{r}: ссылка разорвана переносом строки — Obsidian её не видит"
            for _ in re.findall(r"\[\[[^\]\n]*\n", body)]
    bad += [f"{r}: ссылка Markdown {m}, а не Obsidian"
            for m in re.findall(r"\]\((?![a-z]+:)[^)\s]*\.md(?:#[^)]*)?\)", body)]
    # [текст](что-то) без схемы Obsidian тоже ищет заметкой; нет её — фантомный узел в графе
    bad += [f"{r}: ссылка Markdown {m.group(0)} — в никуда"
            for m in re.finditer(r"\[[^\]\n]*\]\((?![a-z]+:|#)([^)\s]+)\)", body)
            if not resolve(unquote(m.group(1).split("#")[0])) and not (p.parent / unquote(m.group(1))).exists()]
    for target, anchor in LINK.findall(body):
        target = target.replace("\\", "").strip()
        hit = pick(resolve(target), r.lower()) if target else [r.lower()]   # [[#Раздел]] — свой документ
        top = pick(hit, "")   # куда та же ссылка ведёт без поправки на папку
        if not hit:
            bad.append(f"{r}: [[{target}]] — в никуда")
        elif len(hit) > 1 and (hit[0] != top[0] or len(top[0]) == len(top[1])):
            # отсюда ссылка ведёт не туда, куда из других мест, или выбор — случайность сортировки
            bad.append(f"{r}: [[{target}]] — неоднозначно: {', '.join(hit)}; нужен хвост пути")
        elif anchor and hit[0].endswith(".md"):
            heads, blocks = anchors(known[hit[0]].read_text(encoding="utf-8").replace("\r\n", "\n"))
            a = anchor.split("#")[-1].strip()
            if not (a[1:] in blocks if a.startswith("^") else a in heads):
                bad.append(f"{r}: [[{target}#{anchor}]] — нет такого раздела или метки")
    if t == "issue":
        tasks[r] = fm
    if "/история/" in "/" + r:
        continue   # история — только ссылки и якоря
    if t in SIZE_KB and p.stat().st_size > SIZE_KB[t] * 1024:
        notes.append(f"{r}: больше {SIZE_KB[t]} КБ — разрезать или закрытое в историю")
    # таблицы: шапку и код вырезать, номера строк сохранить
    rows = re.sub(r"\A---\n.*?\n---|```.*?```", lambda m: "\n" * m.group(0).count("\n"), text, flags=re.S).split("\n")
    head = None
    for i, line in enumerate(rows):
        if not line.strip().startswith("|"):
            head = None
        elif head is None:   # заголовок — строка, за которой идёт разделитель
            if i + 1 < len(rows) and re.fullmatch(r"[|\s:]*-[|\s:-]*", rows[i + 1]):
                head = cells(line)
        elif cells(line) != head:
            bad.append(f"{r}:{i + 1}: в строке таблицы {cells(line)} ячеек, в заголовке {head}")

# задачи: где лежит, depends, touches, заявки
is_path = lambda x: "/" in x or bool(re.search(r"\.\w+$", x))   # остальное — общий ресурс вне git
inside = lambda x, y: (x.rstrip("/") + "/").lower().startswith((y.rstrip("/") + "/").lower())
task_files, active = {r.lower() for r in tasks}, []
for r, fm in tasks.items():
    closed, st = "/история/" in "/" + r, fm.get("status")
    if closed != (st in CLOSED):
        bad.append(f"{r}: закрытая задача лежит в истории, открытая — нет")
    for d in items(fm.get("depends")):
        hit = pick(resolve(d.strip("[]").split("|")[0]), r.lower())
        if not hit or hit[0] not in task_files:
            bad.append(f"{r}: depends ведёт не на задачу — {d}")
    if closed:
        continue
    bad += [f"{r}: путь из touches не существует — {x}"
            for x in items(fm.get("touches")) if is_path(x) and not (ROOT / x).exists()]
    if st == "in-progress":
        active.append((r, fm))
        ct = subprocess.run(["git", "-C", str(ROOT), "log", "-1", "--format=%ct", "--", r],
                            capture_output=True, text=True).stdout.strip()
        if ct and time.time() - int(ct) > CLAIM_HOURS * 3600:
            notes.append(f"{r}: заявка протухла — {fm.get('assignee')}, коммитов по файлу нет дольше {CLAIM_HOURS} ч")
for i, (r1, f1) in enumerate(active):
    for r2, f2 in active[i + 1:]:
        both = {x for x in items(f1.get("touches")) for y in items(f2.get("touches")) if inside(x, y) or inside(y, x)}
        if both and f1.get("assignee") != f2.get("assignee"):
            notes.append(f"две взятые задачи трогают одно ({', '.join(sorted(both))}): {r1}; {r2}")

print("\n".join(bad + [f"справочно: {n}" for n in notes]) or "находок нет")
sys.exit(1 if bad else 0)
```
