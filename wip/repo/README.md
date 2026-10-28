# Zambia: law history in git

The law of Zambia as a git history: one file per provision, one commit per law on the day it took effect, and the law that made each change as the commit's author. `git blame` names the law behind every paragraph; `git log` lists every change to a provision; `tools/on.py` gives the text in force on any day.

It follows the shared design of [lexifina/global-law](https://github.com/lexifina/global-law), which places it at `zm/`. Every version is a dated point-in-time version published by [ZambiaLII](https://zambialii.org) on the Laws.Africa Peachjam platform.

**What is in it now**

| Folder | Act | Versions | History |
| --- | --- | ---: | --- |
| `constitution/` | [Constitution of Zambia Act, 1991](https://zambialii.org/akn/zm/act/1991/1) | 4 | 1996-12-31 to 2025-12-18 |
| `data-protection/` | [Data Protection Act, 2021](https://zambialii.org/akn/zm/act/2021/3) | 1 | 2021-04-01 to 2021-04-01 |
| `lands/` | [Lands Act](https://zambialii.org/akn/zm/act/1995/29) | 3 | 1996-12-31 to 2016-01-01 |
| `anti-terrorism/` | [Anti-Terrorism and Non-Proliferation Act, 2018](https://zambialii.org/akn/zm/act/2018/6) | 3 | 2018-07-31 to 2024-12-26 |

**Constitution of Zambia Act, 1991**

| In force | Author |
| --- | --- |
| 1996-12-31 | publisher (ZambiaLII): oldest version available |
| 2009-08-31 | Act 20 of 2009 |
| 2016-01-05 | Act 2 of 2016 |
| 2025-12-18 | Act 13 of 2025 |

**Data Protection Act, 2021**

| In force | Author |
| --- | --- |
| 2021-04-01 | Act 3 of 2021 (as enacted) |

**Lands Act**

| In force | Author |
| --- | --- |
| 1996-12-31 | publisher (ZambiaLII): oldest version available |
| 2010-11-19 | Act 41 of 2010 |
| 2016-01-01 | Act 20 of 2015 |

**Anti-Terrorism and Non-Proliferation Act, 2018**

| In force | Author |
| --- | --- |
| 2018-07-31 | Act 6 of 2018 (as enacted) |
| 2023-04-18 | Act 6 of 2023 |
| 2024-12-26 | Act 30 of 2024 |

Each folder's `README.md` lists every provision, how often it changed and when.

## A lawyer's questions as git commands

| Question | Command |
| --- | --- |
| What did sec-001 say on 1996-12-31? | `python tools/on.py 1996-12-31 constitution 1` |
| The same, with raw git (bash) | `git show $(git rev-list -1 --before="1996-12-31T23:59:59Z" main -- constitution/sec-001.md):constitution/sec-001.md` |
| The same, in PowerShell | `$r = git rev-list -1 --before="1996-12-31T23:59:59Z" main -- constitution/sec-001.md; git show "$($r):constitution/sec-001.md"` |
| Which law wrote each line? | `git blame constitution/sec-001.md` |
| Every change, word by word | `git log -p --word-diff constitution/sec-001.md` |
| Every law in the record, in order | `git log --reverse --format="%ad %an" --date=short main` |
| Everything one law changed | `git show law/<key>` (tags `law/<key>` mark each law's commit) |
| The whole act on a date | `python tools/on.py 1996-12-31 constitution` |
| Which law gave a provision its wording on a date | `python tools/on.py --law 1996-12-31 constitution sec-001` |

After a rebuild, refresh tags with `git fetch --force --tags`: a plain fetch keeps stale tags.

## Dates

- Each commit is dated at **noon, Africa/Lusaka, on the day the change took effect**. The day is also in the `In-force:` trailer, which the tools read; enactment (assent) and Gazette publication dates are trailers too, where ZambiaLII states them.
- **The day is ZambiaLII's.** Each version is a Laws.Africa expression, and its date is the day the amendment it takes in came into force, as the amendment list says ("[Amended by <Act> on <date>]"). For a consolidation (a revised edition) it is the date the edition is as at. An act's original expression is dated by its Gazette publication; where ZambiaLII gives a later commencement date ("Commenced on ..."), the first version is dated by that instead (see REPRODUCE.md, decisions).
- `--before="YYYY-MM-DD"` alone uses your clock's time of day, so a law that took effect that day may be missed before noon. Use `T23:59:59Z` as above, or the tool.

## How it is checked

- Every version is read back from git on the day it took effect and on the day before (`tools/check_repo.py`); both must match `corpus.json`. Results are in `REPRODUCE.md`.
- **Against ZambiaLII today:** the last version of each act is ZambiaLII's current expression, as named by its own legislation listing on the retrieval day, and is the text of that expression page.
- **Every version is its own dated expression**: each was parsed from an archived copy of exactly that expression's page, whose sha256 is recorded with the version.
- The repository is rebuilt from the same data a second time and must give identical hashes.

## What "author" means

The author of a commit is the law that made the change, with an e-mail address that cannot exist, so `git blame` and `git log --author` name laws. The committer is always Lexifina.

- **Credits come only from ZambiaLII's own notes.** A version whose History entry names one amending Act is credited to it. Where one version takes in several Acts, or a revised edition, a provision is credited to an Act only if ZambiaLII's editorial note in that provision names it ("[section 5 amended by section 2 of Act 3 of 2020]"); the rest are committed by the publisher and labelled "unexplained", and the commit message names the Acts the version takes in.
- **The first commit** is the act as enacted where that is the oldest version; otherwise it is the oldest version available (a consolidation), credited to the publisher.
- Blame credits whole lines (one paragraph per line). Use `git log -p --word-diff` to see exactly which words each change made.

## What it does not show

- **Only the versions ZambiaLII publishes.** Changes before its oldest version are not separate commits.
- **Editorial notes.** ZambiaLII's bracketed notes ("[Act No. 18 of 1996]", "[section 5 amended by ...]") are left out of the text and used only for credits, except where a provision has no other text (repealed or spent), where the note is what ZambiaLII prints and is kept.
- **Headings above the provision** (Part, Chapter, Division) are left out; each file starts with its own number and heading. Footnotes are kept at the end of the file.
- **Amendments not yet applied.** Where the LII lists an amendment as not yet applied to its consolidated text, it is not in this history; REPRODUCE.md lists each one.
- **No OCR.** Acts the LII shows only as scanned PDFs are not included.

## How it is built


## Sources

| Source | What it gives | Used for |
| --- | --- | --- |
| [ZambiaLII](https://zambialii.org) | Dated point-in-time versions (expressions) of each act, its History and amendment list, and per-provision editorial notes; its listing page names the current version | The text and dates of every version |
| [Internet Archive](https://web.archive.org/) | Archived copies of those expression pages | Reading them |

## Licence

See [LICENSE](LICENSE). Source: ZambiaLII (https://zambialii.org), licensed under the Creative Commons Attribution-NonCommercial 4.0 International licence (CC BY-NC 4.0).

ZambiaLII's terms: CC BY-NC 4.0, crediting ZambiaLII as the source (https://zambialii.org/terms-of-use/). Lexifina's arrangement, messages, tables and tools are CC0.

This repository is not legal advice. Zambia's laws are published in English, so there is no separate summary in another language.
